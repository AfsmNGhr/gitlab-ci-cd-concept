FROM python:3.9.2-alpine3.12

COPY *.txt /

RUN apk update && \
    apk add --no-cache bash coreutils findutils git curl docker-cli openssh pigz && \
    rm -rf /usr/share/man /tmp/* /var/cache/apk/* /var/log/* ~/.cache

RUN apk add --no-cache --virtual build-deps build-base libffi-dev openssl-dev python3-dev cargo && \
    pip install --no-cache-dir -r requirements.txt -r requirements.swarm.txt && \
    find /usr/lib* /usr/local/lib* \
         \( -type d -a -name '__pycache__' -o -name '(test|tests)' \) \
         -o \( -type f -a -name '(*.pyc|*.pxd)' -o -name '(*.pyo|*.pyd)' \) \
         -exec rm -rf '{}' + && \
    find /usr/lib* /usr/local/lib* -name '*.so' -print \
         -exec sh -c 'file "{}" | grep -q "not stripped" && strip -s "{}"' \; && \
    apk del build-deps && \
    rm -rf /usr/share/man /tmp/* /var/cache/apk/* /var/log/* ~/.cache

CMD bash
