FROM --platform=linux/amd64 node:20.11.1-alpine as node
FROM --platform=linux/amd64 python:3.12.2-alpine as python
FROM --platform=linux/amd64 haskell:9.4.8-slim


RUN apt-get update && \
    apt-get install -y --purge --no-install-recommends \
    curl \
    gpg \
    sudo \
    wget \
    git \
    openssh-client && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/* && \
    install -dm 755 /etc/apt/keyrings

ARG USER

RUN useradd -m -s /bin/bash $USER && \
    echo "$USER ALL=(ALL:ALL) NOPASSWD:ALL" > /etc/sudoers
USER $USER

COPY --from=node /usr/local/bin /usr/local/bin
COPY --from=node /usr/local/lib/node_modules/npm /usr/local/lib/node_modules/npm

COPY --from=python /usr/local/bin /usr/local/bin
COPY --from=python /usr/local/lib /usr/local/lib
COPY --from=python /usr/local/include /usr/local/include


ENV TZ=Asia/Tokyo

RUN curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | BOOTSTRAP_HASKELL_NONINTERACTIVE=1 BOOTSTRAP_HASKELL_GHC_VERSION=9.4.8 BOOTSTRAP_HASKELL_CABAL_VERSION=3.8.1.0 sh
ENV PATH="${PATH}:/home/$USER/.ghcup/bin:/home/$USER/.cabal/bin:/home/$USER/.ghc/bin:/home/$USER/.ghcup/hls/2.7.0.0/bin"
RUN ghcup install hls 2.7.0.0

RUN cd /home/$USER && \
    curl -LO https://github.com/neovim/neovim/releases/download/v0.9.5/nvim.appimage && \
    chmod u+x nvim.appimage && \
    ./nvim.appimage --appimage-extract && \
    sudo ln -s /home/$USER/squashfs-root/AppRun /usr/bin/nvim && \
    rm ./nvim.appimage

