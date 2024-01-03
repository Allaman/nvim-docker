<h1 align="center">Nvim-Docker</h1>


<div align="center">
  <p>
[![base-latest](https://github.com/Allaman/nvim-docker/actions/workflows/base-latest.yml/badge.svg)](https://github.com/Allaman/nvim-docker/actions/workflows/base-latest.yml)
[![base-stable](https://github.com/Allaman/nvim-docker/actions/workflows/base-stable.yml/badge.svg)](https://github.com/Allaman/nvim-docker/actions/workflows/base-stable.yml)
[![full-latest](https://github.com/Allaman/nvim-docker/actions/workflows/full-latest.yml/badge.svg)](https://github.com/Allaman/nvim-docker/actions/workflows/full-latest.yml)
[![full-stable](https://github.com/Allaman/nvim-docker/actions/workflows/full-stable.yml/badge.svg)](https://github.com/Allaman/nvim-docker/actions/workflows/full-stable.yml)
  </p>
</div>

A repo containing the source for my Neovim Docker images

- [Base](./base) - a minimal Neovim built from source on Debian (~ **50 MB** compressed -> [Dockerhub](https://hub.docker.com/r/allaman/nvim-base))
- [Full](.full) - opinionated image for my [Neovim config](https://github.com/Allaman/nvim/) (~ **300 MB** compressed -> [Dockerhub](https://hub.docker.com/r/allaman/nvim-full))

Each of the flavor is built for

- **stable** and **HEAD** Neovim
- **linux/amd64** and **linux/arm64** (no virtualization for Docker Desktop on Apple Silicone required)
- triggered **nightly**

## Why Debian as base

You could save some MB with an even more minimal distribution like Alpine. In my opinion, Debian is the sweet spot of stability, packages, and minimalism.
By using Debian as the base image, I must not make a compromise when using this image as the base for other images.

## Usage

### As base image

Use in your own Dockerfile as usual:

```Dockerfile
ARG ARCH
FROM ${ARCH}allaman/nvim-base:stable
```

### As dockerized Neovim

```sh
docker run -it --name nvim --rm --entrypoint /bin/bash nvim-base:stable
docker run -it --name nvim --rm --mount type=bind,source="$(pwd)",target=/home/nvim/work nvim-full:stable
```

### Local Building

The provided [Taskfile](./Taskfile.yml) ([Task](https://taskfile.dev/) is required) allows you to conveniently build the images locally.

Just run `task` to get an overview.
