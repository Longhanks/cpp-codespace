FROM ubuntu:22.04

RUN \
  DEBIAN_FRONTEND=noninteractive apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get -y upgrade --no-install-recommends && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
    autoconf \
    autoconf-archive \
    automake \
    make \
    libc6-dev \
    libtool \
    curl \
    gdb \
    git \
    pkg-config \
    unzip \
    wget \
    zip && \
  wget -nv https://github.com/Kitware/CMake/releases/download/v3.30.3/cmake-3.30.3-linux-x86_64.sh && \
  chmod +x ./cmake-3.30.3-linux-x86_64.sh && \
  ./cmake-3.30.3-linux-x86_64.sh --prefix=/usr/local --skip-license && \
  rm -f cmake-3.30.3-linux-x86_64.sh && \
  wget -qO- https://apt.llvm.org/llvm-snapshot.gpg.key | tee /etc/apt/trusted.gpg.d/apt.llvm.org.asc && \
  echo "deb http://apt.llvm.org/jammy/ llvm-toolchain-jammy-19 main" > /etc/apt/sources.list.d/llvm-toolchain-jammy-19.list && \
  DEBIAN_FRONTEND=noninteractive apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
    clang-19 \
    clang-tools-19 && \
  wget -nv https://github.com/ninja-build/ninja/releases/download/v1.12.1/ninja-linux.zip && \
  unzip ninja-linux.zip && \
  mv ninja /usr/local/bin/ninja && \
  rm -rf ninja-linux.zip && \
  git clone https://github.com/rui314/mold && \
  cd mold && \
  git checkout v2.33.0 && \
  mkdir build && \
  cd build && \
  cmake .. -DCMAKE_C_COMPILER=clang-19 -DCMAKE_CXX_COMPILER=clang++-19 -DCMAKE_BUILD_TYPE=Release -GNinja && \
  ninja && \
  ninja install && \
  cd ../.. && \
  rm -rf mold
