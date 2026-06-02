# GHCR Whoami Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add a minimal custom image based on `traefik/whoami` and publish it to GHCR from GitHub Actions.

**Architecture:** The repository gets a single Dockerfile that extends `traefik/whoami` without changing runtime behavior. A dedicated workflow builds that Dockerfile on pushes to `main` and on manual dispatch, then publishes immutable and rolling tags to GHCR.

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

**Step 1: Trigger on `main` and manual dispatch**

Add `push` on `main` and `workflow_dispatch`.

**Step 2: Compute tags**

Publish `latest` and `sha-<shortsha>`.

**Step 3: Login and push**

Use `docker/login-action` and `docker/build-push-action`.

### Task 3: Document usage

**Files:**
- Modify: `README.md`

**Step 1: Document the image name**

Explain that the image is published to `ghcr.io/<owner>/portainertest-whoami`.

**Step 2: Document Portainer variables**

Explain `APP_IMAGE` and `SERVICE_TAG`.
