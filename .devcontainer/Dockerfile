FROM haskell:latest

ENV PATH="${PATH}:/root/.ghcup/bin:/root/.cabal/bin:/root/.ghc/bin" \
    BOOTSTRAP_HASKELL_NONINTERACTIVE=1

RUN curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | BOOTSTRAP_HASKELL_NONINTERACTIVE=1 BOOTSTRAP_HASKELL_GHC_VERSION=9.4.5 BOOTSTRAP_HASKELL_CABAL_VERSION=3.8.1.0 BOOTSTRAP_HASKELL_INSTALL_NO_STACK=1 sh


RUN chsh -s /bin/bash
RUN apt update && apt upgrade -y
RUN apt install -y curl

RUN apt update -y && apt install -y gpg sudo wget
RUN install -dm 755 /etc/apt/keyrings

ENV TZ=Asia/Tokyo

RUN wget -qO - https://mise.jdx.dev/gpg-key.pub | gpg --dearmor | tee /etc/apt/keyrings/mise-archive-keyring.gpg 1> /dev/null
# RUN echo "deb [signed-by=/etc/apt/keyrings/mise-archive-keyring.gpg arch=amd64] https://mise.jdx.dev/deb stable main" | sudo tee /etc/apt/sources.list.d/mise.list
RUN echo "deb [signed-by=/etc/apt/keyrings/mise-archive-keyring.gpg arch=arm64] https://mise.jdx.dev/deb stable main" | sudo tee /etc/apt/sources.list.d/mise.list
RUN apt update && apt install -y mise

RUN echo 'eval "$(mise activate bash)"' >> ~/.bashrc

RUN mise i node@20.11.1 && mise use -g node@latest

RUN mise i python@3.12.2 && mise use -g python@latest

