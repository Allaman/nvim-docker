# NVIM-DOCKER 
[![base-latest](https://github.com/Allaman/nvim-docker/actions/workflows/base-latest.yml/badge.svg)](https://github.com/Allaman/nvim-docker/actions/workflows/base-latest.yml)
[![base-stable](https://github.com/Allaman/nvim-docker/actions/workflows/base-stable.yml/badge.svg)](https://github.com/Allaman/nvim-docker/actions/workflows/base-stable.yml)
[![full-latest](https://github.com/Allaman/nvim-docker/actions/workflows/full-latest.yml/badge.svg)](https://github.com/Allaman/nvim-docker/actions/workflows/full-latest.yml)
[![full-stable](https://github.com/Allaman/nvim-docker/actions/workflows/full-stable.yml/badge.svg)](https://github.com/Allaman/nvim-docker/actions/workflows/full-stable.yml)


A repo containing the source for my Neovim Docker images

- [Base](./base) - a minimal Neovim built form source on Debian (~ **70 MB** uncompressed -> [Dockerhub](https://hub.docker.com/repository/docker/allaman/nvim-base/general))
- [Full](.full) - opinionated image for my [Neovim config](https://github.com/Allaman/nvim/) (~ **1 GB** uncompressed -> [Dockerhub](https://hub.docker.com/repository/docker/allaman/nvim-full/general))

Each of the flavor is built with 

- **stable** and **HEAD** Neovim
- for **linux/amd64** and **linux/arm64** (no virtualization for Docker Desktop on Apple Silicone required)

## Usage

### As base image

Use in your own Dockerfile as usual:

```Dockerfile
ARG ARCH
FROM ${ARCH}nvim-base:stable
```

### As dockerized Neovim

```sh
docker run -it --name nvim --rm --entrypoint /bin/bash nvim-base:stable
docker run -it --name nvim --rm --mount type=bind,source="$(pwd)",target=/home/nvim/wd nvim-full:stable
```

### Local Building

The provided [Taskfile](./Taskfile.yml) ([Task](https://taskfile.dev/) is required) allows you to conveniently build the images locally. Just run `task` to get an overview.
