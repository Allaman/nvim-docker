ARG ARCH
FROM ${ARCH}debian:stable-slim as builder

ARG TARGETOS
ARG TARGETARCH

ARG BRANCH

# Install dependencies and build Neovim from source
RUN apt-get update \
&& apt-get install --no-install-recommends -y \
  ca-certificates \
  cmake \
  g++ \
  gettext \
  git \
  make \
  ninja-build \
  unzip \
  wget \
&& rm -rf /var/lib/apt/lists/* \
&& git clone -b ${BRANCH} https://github.com/neovim/neovim /tmp/neovim \
&& cd /tmp/neovim \
&& make CMAKE_BUILD_TYPE=RelWithDebInfo && make install && rm -fr /tmp/neovim

FROM ${ARCH}debian:stable-slim

ENV LANGUAGE=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

# install locales to prevent UTF-8 warnings
RUN apt-get update \
&& apt-get install --no-install-recommends -y \
locales \
sudo \
&& sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen && dpkg-reconfigure --frontend=noninteractive locales

# Copy Neovim from builder image
RUN mkdir -p /usr/local/share/nvim
COPY --from=builder /usr/local/bin/nvim /usr/local/bin
COPY --from=builder /usr/local/lib/nvim /usr/local/lib
COPY --from=builder /usr/local/share/nvim/ /usr/local/share/nvim

# Add user 'nvim' and allow passwordless sudo
RUN adduser --disabled-password --gecos '' nvim \
&& adduser nvim sudo \
&& echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# switch to a the unpriviledged user
USER nvim
WORKDIR /home/nvim

ENTRYPOINT ["/bin/bash", "-c", "nvim"]
