FROM ubuntu:22.04

RUN \
  wget -nv https://github.com/Kitware/CMake/releases/download/v3.30.2/cmake-3.30.2-linux-x86_64.sh && \
  chmod +x ./cmake-3.30.2-linux-x86_64.sh && \
  ./cmake-3.30.2-linux-x86_64.sh --prefix=/usr/local --skip-license && \
  rm -f cmake-3.30.2-linux-x86_64.sh && \
  DEBIAN_FRONTEND=noninteractive apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
    autoconf \
    autoconf-archive \
    automake \
    make \
    libc6-dev \
    libtool \
    curl \
    git \
    pkg-config \
    unzip \
    zip && \
  wget -qO- https://apt.llvm.org/llvm-snapshot.gpg.key | tee /etc/apt/trusted.gpg.d/apt.llvm.org.asc && \
  echo "deb http://apt.llvm.org/bookworm/ llvm-toolchain-bookworm-18 main" > /etc/apt/sources.list.d/llvm-toolchain-bookworm-18.list && \
  DEBIAN_FRONTEND=noninteractive apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y \
    clang-18 \
    clang-tools-18 && \
  git clone https://github.com/rui314/mold && \
  cd mold && \
  git checkout v2.33.0 && \
  mkdir build && \
  cd build && \
  cmake .. -DCMAKE_C_COMPILER=clang-18 -DCMAKE_CXX_COMPILER=clang++-18 -DCMAKE_BUILD_TYPE=Release -GNinja && \
  ninja && \
  ninja install && \
  cd ../.. && \
  rm -rf mold
