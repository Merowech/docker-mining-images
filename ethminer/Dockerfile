FROM nvidia/cuda:9.0-devel

WORKDIR /eth/

# Package and dependency setup
RUN apt-get update \
    && apt-get -y install software-properties-common \
    && add-apt-repository -y ppa:ethereum/ethereum -y \
    && apt-get update \
    && apt-get install -y git \
     cmake \
     libcryptopp-dev \
     libleveldb-dev \
     libjsoncpp-dev \
     libjsonrpccpp-dev \
     libboost-all-dev \
     libgmp-dev \
     libreadline-dev \
     libcurl4-gnutls-dev \
     ocl-icd-libopencl1 \
     opencl-headers \
     mesa-common-dev \
     libmicrohttpd-dev \
     python \
     python-twisted \
     build-essential

# Git repo set up
RUN git clone https://github.com/ethereum-mining/ethminer.git;

# Build
RUN cd ethminer; \
    git submodule update --init --recursive; \
    mkdir build; \
    cd build; \
    cmake .. -DETHASHCUDA=ON -DETHASHCL=OFF -DETHSTRATUM=ON; \
    cmake --build .; \
    make install;

RUN cd /eth/

# Git repo set up
RUN git clone https://github.com/Atrides/eth-proxy.git;
RUN cd eth-proxy; \
    sed -r -i "s/XXXXXX/0x72907f514Fe5D1bbBef776EADD146f64D0b8d6D4/" eth-proxy.conf; \
    sed -r -i "s/MONITORING = False/MONITORING = True/" eth-proxy.conf; \
    sed -r -i "s/mail@example.com/dienerdeslich@gmail.com/" eth-proxy.conf;

# Env setup
ENV GPU_FORCE_64BIT_PTR=0
ENV GPU_MAX_HEAP_SIZE=100
ENV GPU_USE_SYNC_OBJECTS=1
ENV GPU_MAX_ALLOC_PERCENT=100
ENV GPU_SINGLE_ALLOC_PERCENT=100

# ENTRYPOINT "python /eth/eth-proxy/eth-proxy.py"
CMD ["ethminer --farm-recheck 200 -U -F http://127.0.0.1:8080/miner"


