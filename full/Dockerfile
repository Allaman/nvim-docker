ARG ARCH
ARG BASE_IMAGE
FROM ${ARCH}${BASE_IMAGE}

ARG TARGETOS
ARG TARGETARCH

# Install opionionated tools
RUN apt-get update \
&& apt-get install --no-install-recommends -y \
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
  sudo \
  tar \
  unzip \
  wget \
  zip \
&& rm -rf /var/lib/apt/lists/* \
&& ln -s "$(which fdfind)" /usr/bin/fd \
&& ln -s "$(which python3)" /usr/bin/python \
&& curl -sLo go.tar.gz "https://go.dev/dl/go1.21.0.linux-${TARGETARCH}.tar.gz" \
&& tar -C /usr/local/bin -xzf go.tar.gz \
&& rm go.tar.gz

ENV PATH=$PATH:/usr/local/bin/go/bin/
ENV GOPATH=/home/nvim/.local/share/go
ENV PATH=$PATH:$GOPATH/bin

# Add user 'nvim' and allow passwordless sudo
RUN adduser --disabled-password --gecos '' nvim \
&& echo '%ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# switch to the unpriviledged user
USER nvim
WORKDIR /home/nvim

ENTRYPOINT ["/bin/bash", "-c", "nvim"]
