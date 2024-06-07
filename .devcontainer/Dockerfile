FROM --platform=linux/amd64 haskell:9.4.8-slim

RUN chsh -s /bin/bash
RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y curl


RUN apt-get install -y gpg sudo wget git openssh-client
RUN install -dm 755 /etc/apt/keyrings

RUN curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | BOOTSTRAP_HASKELL_NONINTERACTIVE=1 BOOTSTRAP_HASKELL_GHC_VERSION=9.4.8 BOOTSTRAP_HASKELL_CABAL_VERSION=3.8.1.0 sh

ENV PATH="${PATH}:/root/.ghcup/bin:/root/.cabal/bin:/root/.ghc/bin:/root/.ghcup/hls/2.7.0.0/bin"
RUN ghcup install hls 2.7.0.0

ENV TZ=Asia/Tokyo

RUN wget -qO - https://mise.jdx.dev/gpg-key.pub | gpg --dearmor | tee /etc/apt/keyrings/mise-archive-keyring.gpg 1> /dev/null
RUN echo "deb [signed-by=/etc/apt/keyrings/mise-archive-keyring.gpg arch=amd64] https://mise.jdx.dev/deb stable main" | sudo tee /etc/apt/sources.list.d/mise.list
RUN apt-get update && apt-get install -y mise

RUN echo 'eval "$(mise activate bash)"' >> ~/.bashrc

RUN mise i node@20.11.1 && mise use -g node@latest

RUN mise i python@3.12.2 && mise use -g python@latest

# install neovim 0.9.5 appimage
RUN curl -LO https://github.com/neovim/neovim/releases/download/v0.9.5/nvim.appimage
RUN chmod u+x nvim.appimage
RUN ./nvim.appimage --appimage-extract
RUN ln -s /squashfs-root/AppRun /usr/bin/nvim
