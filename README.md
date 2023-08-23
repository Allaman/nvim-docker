# NVIM-DOCKER

A repo containing the source for my Neovim Docker images

- [Base](./base) for a minimal Neovim built form source on Debian (~ **70 MB**)
- [Full](.full) an opinionated image for my [Neovim config](https://github.com/Allaman/nvim/) (~ **1 GB**)

Each of the flavor is built with stable and HEAD Neovim.

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

### Build locally

The provided [Taskfile](./Taskfile.yml) ([Task](https://taskfile.dev/) is required) allows you to conveniently build the images locally. Just run `task` to get an overview.
