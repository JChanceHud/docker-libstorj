FROM alpine:latest
MAINTAINER Chance Hudson

WORKDIR /root
ENV TMPDIR=/tmp

# Build dependencies, removed after build
RUN apk add --no-cache --virtual .build-deps \
  automake \
  make \
  git \
  autoconf \
  g++ \
  && \
  apk add --no-cache \
  libtool \
  libmicrohttpd-dev \
  curl-dev \
  nettle-dev \
  json-c-dev \
  libuv-dev && \
  git clone -b 1.0.0 https://github.com/Storj/libstorj.git

WORKDIR /root/libstorj

RUN ./autogen.sh && \
  ./configure && \
  make && \
  make install && \
  apk del .build-deps && \
  ./test/tests

WORKDIR /

RUN rm -rf /root/libstorj

CMD ["/usr/local/bin/storj"]
