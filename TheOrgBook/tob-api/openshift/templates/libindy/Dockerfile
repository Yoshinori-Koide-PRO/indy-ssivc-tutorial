FROM ubuntu:16.04

# Install environment
RUN apt-get update -y && \
apt-get install -y \
    git \
    curl \
    build-essential \
    pkg-config \
    cmake \
    libssl-dev \
    libsqlite3-dev \
    libsodium-dev

ENV HOME=/opt/app-root/src
WORKDIR $HOME

# Install rust toolchain
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain 1.26.0

# Build libindy
RUN git clone https://github.com/hyperledger/indy-sdk.git
WORKDIR $HOME/indy-sdk/libindy
RUN git fetch
RUN git checkout 778a38d92234080bb77c6dd469a8ff298d9b7154
RUN $HOME/.cargo/bin/cargo build

# Move libindy to lib path
RUN mv target/debug/libindy.so /usr/lib

WORKDIR $HOME
