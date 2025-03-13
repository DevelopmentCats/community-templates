---
display_name: Docker with Cursor IDE & Node.js
description: Development environment with Docker, Cursor IDE, and Node.js for JavaScript/TypeScript projects
icon: ../../../site/static/icon/docker.png
maintainer_github: DevelopmentCats
verified: false
tags: [docker, cursor, nodejs]
---

# Remote Development with Cursor IDE and Node.js on Docker

Provision Docker containers with [Cursor IDE](https://cursor.sh/) and Node.js as [Coder workspaces](https://coder.com/docs/workspaces) for JavaScript and TypeScript development.

## Prerequisites

### Infrastructure

The VM you run Coder on must have a running Docker socket and the `coder` user must be added to the Docker group:

```sh
# Add coder user to Docker group
sudo adduser coder docker

# Restart Coder server
sudo systemctl restart coder

# Test Docker
sudo -u coder docker ps
```

## Architecture

This template provisions the following resources:

- Docker image (built by Docker socket and kept locally)
- Docker container pod (ephemeral)
- Docker volume (persistent on `/home/coder`)
- Cursor IDE (for modern JavaScript and AI-assisted development)
- Node.js runtime (for JavaScript and TypeScript development)
- Git repository cloning (for immediate access to your code)

This means, when the workspace restarts, any tools or files outside of the home directory are not persisted. To pre-bake tools into the workspace (e.g. `python3`), modify the container image. Alternatively, individual developers can [personalize](https://coder.com/docs/dotfiles) their workspaces with dotfiles.

## Features

### Cursor IDE

This template automatically installs and configures [Cursor](https://cursor.sh/), a modern code editor built on VSCode with AI capabilities. Cursor will automatically open to your cloned Git repository.

### Node.js

Node.js is pre-installed in the workspace, providing full JavaScript and TypeScript development support. This allows you to:
- Run JavaScript/TypeScript applications
- Install npm packages
- Use Node.js tooling like npm, yarn, or pnpm
- Develop and test web applications

### Git Repository

When creating a workspace, you'll be prompted for a Git repository URL. The repository will be automatically cloned into `/home/coder/workspace/[repo-name]` and Cursor will open directly to this folder.

> **Note**
> This template is designed to be a starting point! Edit the Terraform to extend the template to support your use case.

### Editing the image

Edit the `Dockerfile` and run `coder templates push` to update workspaces.

---
