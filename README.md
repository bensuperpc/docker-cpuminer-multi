Supported tags and respective `Dockerfile` links
================================================

  * [`alpine`, `alpine-latest` (Dockerfile)](https://github.com/bensuperpc/docker-cpuminer-multi/blob/master/alpine/Dockerfile) [![](https://images.microbadger.com/badges/image/bensuperpc/docker-cpuminer-multi.svg)](https://microbadger.com/images/bensuperpc/docker-cpuminer-multi "Get your own image badge on microbadger.com")
  * [`debian`, `latest` (Dockerfile)](https://github.com/bensuperpc/docker-cpuminer-multi/blob/master/debian/Dockerfile) [![](https://images.microbadger.com/badges/image/bensuperpc/docker-cpuminer-multi.svg)](https://microbadger.com/images/bensuperpc/docker-cpuminer-multi "Get your own image badge on microbadger.com")
  * [`archlinux`,`archlinux-latest` (Dockerfile)](https://github.com/bensuperpc/docker-cpuminer-multi/blob/master/archlinux/Dockerfile) [![](https://images.microbadger.com/badges/image/bensuperpc/docker-cpuminer-multi.svg)](https://microbadger.com/images/bensuperpc/docker-cpuminer-multi "Get your own image badge on microbadger.com")
  * [`ubuntu`, `ubuntu-latest` (Dockerfile)](https://github.com/bensuperpc/docker-cpuminer-multi/blob/master/ubuntu/Dockerfile) [![](https://images.microbadger.com/badges/image/bensuperpc/docker-cpuminer-multi.svg)](https://microbadger.com/images/bensuperpc/docker-cpuminer-multi "Get your own image badge on microbadger.com")
  * [`fedora`, `fedora-latest` (Dockerfile)](https://github.com/bensuperpc/docker-cpuminer-multi/blob/master/fedora/Dockerfile) [![](https://images.microbadger.com/badges/image/bensuperpc/docker-cpuminer-multi.svg)](https://microbadger.com/images/bensuperpc/docker-cpuminer-multi "Get your own image badge on microbadger.com")

[![docker-cpuminer-multi](https://github.com/bensuperpc/docker-cpuminer-multi/actions/workflows/main.yml/badge.svg)](https://github.com/bensuperpc/docker-cpuminer-multi/actions/workflows/main.yml) <img alt="Docker Pulls" src="https://img.shields.io/docker/pulls/bensuperpc/cpuminer-multi">

What is cpuminer-multi
----------------------

[**tpruvot/cpuminer-multi**](https://github.com/tpruvot/cpuminer-multi) is a multi-threaded CPU miner, fork of pooler's [cpuminer](https://github.com/pooler) and tpruvot's [cpuminer-multi](https://github.com/wernight/docker-cpuminer-multi)  (see AUTHORS for list of contributors).

It can mine almost all crypto currencies using CPU. This means you're a lot less likely to get a block, so
you might want to join a pool like https://www.multipool.us/dashboard/help/


Usage example
-------------
The `:alpine` tag is smaller but some people reported issue with it.
You can test both `:debian` ([Debian](https://hub.docker.com/_/debian)-based)
and `:alpine` ([Linux Alpine](https://hub.docker.com/_/alpine)-based) versions
to check that they work on your machine via:

    $ docker run --rm bensuperpc/cpuminer-multi:latest cpuminer --cputest
    $ docker run --rm bensuperpc/cpuminer-multi:latest cpuminer --benchmark
    $ docker run --rm bensuperpc/cpuminer-multi cpuminer -a cryptonight -o stratum+tcp://xmr.pool.minergate.com:45700 -u <EMail> -p x

To see the CLI help do:

    $ docker run --rm bensuperpc/cpuminer-multi cpuminer --help


Feedbacks
---------

This is an **experimental** image. Please report and try to fix any issues you might encounter.

Suggestions are welcome on our [GitHub issue tracker](https://github.com/bensuperpc/docker-cpuminer-multi/issues).

Original Author : https://github.com/wernight/docker-cpuminer-multi
