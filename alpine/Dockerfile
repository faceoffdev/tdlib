FROM alpine:3.19 as builder

ARG DEBIAN_FRONTEND=noninteractive

RUN apk update && \
    apk upgrade && \
    apk add --update \
    alpine-sdk \
    linux-headers \
    git \
    zlib-dev \
    openssl-dev \
    gperf \
    cmake

RUN cd /tmp && \
    git clone https://github.com/tdlib/td.git

RUN cd /tmp/td && \
    git checkout master && \
    mkdir build && \
    cd build && \
    cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX:PATH=/usr/local .. && \
    cmake --build . --target install


FROM alpine:3.19

COPY --from=builder /usr/local/include/td /usr/local/include/td/
COPY --from=builder /usr/local/lib/libtd* /usr/local/lib/
