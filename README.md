## The concept pipeline for Gitlab CI / CD

Features:

- Full-dockerized & artifactless (use multi-stage build for everything, run scheduled cleanup with ttl)
- Use ansible build & deploy roles
- Reuse action with Trigger API & Project API
- Delayed job with ttl (use lock for only build one at a time)
- Clone database before start Review-App from staging volume
- Release by tag and start deployment on production server
