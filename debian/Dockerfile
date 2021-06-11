ARG DOCKER_IMAGE=debian:bullseye-slim
FROM $DOCKER_IMAGE

RUN set -x \
    # Runtime dependencies.
 && apt-get update \
 && apt-get install -y \
        libcurl4 \
        libgmp10 \
        libjansson4 \
        libssl-dev \
        openssl \
    # Build dependencies.
 && apt-get install -y \
        autoconf \
        automake \
        curl \
        g++ \
        git \
        libcurl4-openssl-dev \
        libjansson-dev \
        libssl-dev \
        libgmp-dev \
        make \
        pkg-config \
        zlib1g-dev \
    # Compile from source code.
 && git clone --recursive https://github.com/tpruvot/cpuminer-multi.git /tmp/cpuminer \
 && cd /tmp/cpuminer \
 && ./autogen.sh \
 && ./configure CFLAGS="-O2 -march=sandybridge -mtune=tigerlake -pipe" --with-crypto --with-curl \
 && make -j$(nproc) install \
    # Install dumb-init (avoid PID 1 issues).
    # https://github.com/Yelp/dumb-init
 && curl -Lo /usr/local/bin/dumb-init "https://github.com/Yelp/dumb-init/releases/download/v1.2.5/dumb-init_1.2.5_amd64.deb" \
 && chmod +x /usr/local/bin/dumb-init \
    # Clean-up
 && cd / \
 && apt-get purge --auto-remove -y \
        autoconf \
        automake \
        curl \
        g++ \
        git \
        libcurl4-openssl-dev \
        libjansson-dev \
        libssl-dev \
        libgmp-dev \
        make \
        pkg-config \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && rm -rf /tmp/* \
    # Verify
 && cpuminer --cputest \
 && cpuminer --version

ENTRYPOINT ["dumb-init"]
CMD ["cpuminer", "--help"]
