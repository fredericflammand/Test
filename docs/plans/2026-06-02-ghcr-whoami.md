# GHCR Whoami Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add a minimal custom image based on `traefik/whoami` and publish it to GHCR from GitHub Actions.

**Architecture:** The repository gets a single Dockerfile that extends `traefik/whoami` without changing runtime behavior. A dedicated manual workflow builds that Dockerfile on demand, then publishes a rolling `latest` tag plus a date-based version tag to GHCR.

**Tech Stack:** Docker, GitHub Actions, GitHub Container Registry

---

### Task 1: Add image source

**Files:**
- Create: `Dockerfile`

**Step 1: Add the base image**

Use `FROM traefik/whoami:latest`.

**Step 2: Add repository metadata**

Set OCI labels for source and description.

**Step 3: Keep runtime unchanged**

Do not override `ENTRYPOINT` or `CMD`.

### Task 2: Add build and publish workflow

**Files:**
- Create: `.github/workflows/build-publish-image.yml`

**Step 1: Trigger on manual dispatch**

Add `workflow_dispatch` only.

**Step 2: Compute tags**

Publish `latest` and `YYYY.M.D.<run_number>`.

**Step 3: Login and push**

Use `docker/login-action` and `docker/build-push-action`.

### Task 3: Document usage

**Files:**
- Modify: `README.md`

**Step 1: Document the image name**

Explain that the image is published to `ghcr.io/<owner>/portainertest-whoami`.

**Step 2: Document Portainer variables**

Explain `APP_IMAGE` and `SERVICE_TAG`.
