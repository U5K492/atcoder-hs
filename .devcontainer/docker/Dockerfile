FROM ubuntu:22.04

RUN chsh -s /bin/bash
RUN apt update && apt upgrade -y
RUN apt install -y curl
RUN apt install -y --no-install-recommends build-essential curl libffi-dev libffi8ubuntu1 libgmp-dev libgmp10 libncurses-dev libncurses5 libtinfo5 llvm-14

RUN apt update -y && apt install -y gpg sudo wget curl
RUN install -dm 755 /etc/apt/keyrings
RUN wget -qO - https://mise.jdx.dev/gpg-key.pub | gpg --dearmor | tee /etc/apt/keyrings/mise-archive-keyring.gpg 1> /dev/null
RUN echo "deb [signed-by=/etc/apt/keyrings/mise-archive-keyring.gpg arch=amd64] https://mise.jdx.dev/deb stable main" | sudo tee /etc/apt/sources.list.d/mise.list
RUN apt update && apt install -y mise

RUN echo 'eval "$(mise activate bash)"' >> ~/.bashrc

RUN mise i node@20.11.1 && mise use -g node@latest
RUN npm install -g atcoder-cli
RUN echo acc

RUN mise i python@3.12.2 && mise use -g python@latest
RUN pip3 install online-judge-tools
RUN echo oj --version

RUN curl --proto '=https' --tlsv1.2 -sSf https://get-ghcup.haskell.org | BOOTSTRAP_HASKELL_NONINTERACTIVE=1 BOOTSTRAP_HASKELL_GHC_VERSION=9.4.5 BOOTSTRAP_HASKELL_CABAL_VERSION=3.8.1.0 BOOTSTRAP_HASKELL_INSTALL_NO_STACK=1 sh
ENV PATH="/root/.ghcup/bin:${PATH}"


WORKDIR /workspace

COPY . /workspace