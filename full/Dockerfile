ARG ARCH
ARG BASE_IMAGE
FROM ${ARCH}${BASE_IMAGE}

ARG TARGETOS
ARG TARGETARCH

# hadolint ignore=DL3004
RUN sudo apt-get update \
&& sudo apt-get install --no-install-recommends -y \
  build-essential \
  ca-certificates \
  curl \
  fd-find \
  fzf \
  git \
  gnupg \
  npm \
  python3-pip \
  ripgrep \
  tar \
  unzip \
  wget \
  zip \
&& sudo rm -rf /var/lib/apt/lists/* \
&& sudo ln -s "$(which fdfind)" /usr/bin/fd \
&& sudo ln -s "$(which python3)" /usr/bin/python \
&& curl -sLo go.tar.gz "https://go.dev/dl/go1.21.0.linux-${TARGETARCH}.tar.gz" \
&& sudo tar -C /usr/local/bin -xzf go.tar.gz \
&& rm go.tar.gz

ENV PATH=$PATH:/usr/local/bin/go/bin/
ENV GOPATH=/home/nvim/.local/share/go
ENV PATH=$PATH:$GOPATH/bin

ENTRYPOINT ["/bin/bash", "-c", "nvim"]
