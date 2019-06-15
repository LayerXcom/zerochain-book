# Installation

## Initial Setup
Setup latest rust environment.

```
curl https://sh.rustup.rs -sSf | sh

rustup update stable
rustup update nightly
rustup target add wasm32-unknown-unknown --toolchain nightly
cargo +nightly install --git https://github.com/alexcrichton/wasm-gc
```

You will also need to install the following packages:
- Mac:
```
brew install cmake pkg-config openssl git llvm
```
- Linux:
```
sudo apt install cmake pkg-config libssl-dev git clang libclang-dev
```

## Building
Zerochan, then, can be building.

```
git clone git@github.com:LayerXcom/zero-chain.git
cd zero-chain
./build.sh
cargo install --force --path ./
```
