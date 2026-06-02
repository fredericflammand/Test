# Portainer Test

This repository builds a custom test image based on `traefik/whoami` and can deploy it through Portainer.

## Published image

- GHCR image: `ghcr.io/<owner>/portainertest-whoami`
- Published tags:
  - `latest`
  - `YYYY.M.D.<run_number>`

## Portainer stack variables

- `APP_IMAGE=ghcr.io/<owner>/portainertest-whoami`
- `SERVICE_TAG=latest` or `YYYY.M.D.<run_number>`
