ARG DOCKER_IMAGE=alpine:3.13
FROM $DOCKER_IMAGE as builder

LABEL author="Bensuperpc <bensuperpc@gmail.com>"
LABEL mantainer="Bensuperpc <bensuperpc@gmail.com>"

ARG VERSION="1.0.0"
ENV VERSION=$VERSION

RUN set -x \
      # Runtime dependencies.
   && apk add --no-cache \
         libcurl \
         libgcc \
         libstdc++ \
         openssl \
      # Build dependencies.
   && apk add --no-cache -t .build-deps \
         autoconf \
         automake \
         build-base \
         curl \
         curl-dev \
         git \
         openssl-dev \
         ccache \
         bash \
      # Compile from source code.
   && git clone --recursive https://github.com/tpruvot/cpuminer-multi.git /tmp/cpuminer \
   && cd /tmp/cpuminer \
   && ./autogen.sh \
   && ./configure CFLAGS="-O2 -march=sandybridge -mtune=tigerlake -pipe" --with-crypto --with-curl || cat config.log \
   && make -j$(nproc) install \
      # Install dumb-init (avoid PID 1 issues).
      # https://github.com/Yelp/dumb-init
   && git clone  --recursive https://github.com/Yelp/dumb-init.git /tmp/dumb-init \
   && cd /tmp/dumb-init \
   && make -j$(nproc) \
   && cp dumb-init /usr/local/bin/dumb-init \
      # Clean-up
   && cd / \
   && apk del --purge .build-deps \
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