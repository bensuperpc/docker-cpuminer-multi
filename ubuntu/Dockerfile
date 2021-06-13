ARG DOCKER_IMAGE=ubuntu:latest
FROM $DOCKER_IMAGE

ARG DEBIAN_FRONTEND=noninteractive

LABEL author="Bensuperpc <bensuperpc@gmail.com>"
LABEL mantainer="Bensuperpc <bensuperpc@gmail.com>"

ARG VERSION="1.0.0"
ENV VERSION=$VERSION

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
         libc6-dev \
         git \
         libcurl4-openssl-dev \
         libjansson-dev \
         libssl-dev \
         libgmp-dev \
         make \
         pkg-config \
         zlib1g-dev \
         ccache \
      # Compile from source code.
   && git clone --recursive https://github.com/tpruvot/cpuminer-multi.git /tmp/cpuminer \
   && cd /tmp/cpuminer \
   && ./autogen.sh \
   && ./configure CFLAGS="-O2 -march=sandybridge -mtune=tigerlake -pipe" --with-crypto --with-curl \
   && make -j$(nproc) install \
      # Install dumb-init (avoid PID 1 issues).
      # https://github.com/Yelp/dumb-init
      && git clone  --recursive https://github.com/Yelp/dumb-init.git /tmp/dumb-init \
      && cd /tmp/dumb-init \
      && make -j$(nproc) \
      && cp dumb-init /usr/local/bin/dumb-init \
      # Clean-up
   && cd / \
   && apt-get purge --auto-remove -y \
         autoconf \
         automake \
         curl \
         g++ \
         gcc \
         git \
         libcurl4-openssl-dev \
         libjansson-dev \
         libssl-dev \
         libgmp-dev \
         libc6-dev \
         make \
         pkg-config \
         ccache \
   && apt-get clean \
   && rm -rf /var/lib/apt/lists/* \
   && rm -rf /tmp/* \
      # Verify
      && cpuminer --cputest \
      && dumb-init --version \
      && cpuminer --version

LABEL org.label-schema.schema-version="1.0" \
   org.label-schema.build-date=$BUILD_DATE \
   org.label-schema.name="bensuperpc/cpuminer-multi" \
   org.label-schema.description="cpuminer-multi in docker" \
   org.label-schema.version=$VERSION \
   org.label-schema.vendor="Bensuperpc" \
   org.label-schema.url="http://bensuperpc.com/" \
   org.label-schema.vcs-url="https://github.com/Bensuperpc/docker-cpuminer-multi" \
   org.label-schema.vcs-ref=$VCS_REF \
   org.label-schema.docker.cmd="docker build -t bensuperpc/cpuminer-multi -f Dockerfile ."

ENTRYPOINT ["dumb-init"]
CMD ["cpuminer", "--help"] 
