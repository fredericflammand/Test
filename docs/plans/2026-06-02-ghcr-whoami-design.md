# GHCR Whoami Design

**Goal:** Build and publish a custom test image based on `traefik/whoami`, then make it available for Portainer deployments.

**Scope:**
- Add a minimal `Dockerfile` that preserves `traefik/whoami` runtime behavior.
- Add a GitHub Actions workflow that builds and pushes the image to GHCR.
- Keep the existing Portainer deployment flow compatible by pointing `APP_IMAGE` to the published image.

**Approach:**
- Use `FROM traefik/whoami:latest` so browser behavior stays unchanged.
- Add lightweight metadata (`LABEL`) to prove the image is built from this repository.
- Publish two tags from GitHub Actions: `latest` and a short-SHA tag.

**Success Criteria:**
- A workflow run pushes `ghcr.io/<owner>/<image>:latest`.
- The same workflow pushes `ghcr.io/<owner>/<image>:sha-<shortsha>`.
- The published image still answers like `traefik/whoami` in a browser.
