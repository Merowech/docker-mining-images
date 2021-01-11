FROM nvidia/cuda:11.1-devel

WORKDIR /eth/

# Package and dependency setup
RUN apt-get update \
    && apt-get -y install software-properties-common \
    && apt-get install -y git \
     cmake \
     perl \
     libdbus-1-dev \
     mesa-common-dev \
     build-essential

# Git repo set up
RUN git clone https://github.com/ethereum-mining/ethminer.git;

# Build
RUN cd ethminer; \
    git submodule update --init --recursive; \
    mkdir build; \
    cd build; \
    cmake .. -DETHASHCUDA=ON -DETHSTRATUM=ON; \
    cmake --build .; \
    make install;

RUN cd /eth/

# Env setup
ENV GPU_FORCE_64BIT_PTR=0
ENV GPU_MAX_HEAP_SIZE=100
ENV GPU_USE_SYNC_OBJECTS=1
ENV GPU_MAX_ALLOC_PERCENT=100
ENV GPU_SINGLE_ALLOC_PERCENT=100

ENTRYPOINT ["/usr/local/bin/ethminer"]


