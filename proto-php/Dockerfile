FROM php:7.1 

RUN /bin/cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo 'Asia/Shanghai' > /etc/timezone

RUN apt-get update \
    && apt-get install -y \
        curl \
        wget \
        git \
        zip \
        libz-dev \
        libssl-dev \
        libnghttp2-dev \
        supervisor \
        libc-ares-dev \
    && apt-get clean \
    && apt-get autoremove

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && composer self-update --clean-backups

RUN docker-php-ext-install -j$(nproc) bcmath

RUN docker-php-ext-install pdo_mysql

COPY ./protobuf-all.tar.gz /protobuf.tar.gz
COPY ./grpc.tar.gz /grpc.tar.gz
RUN mkdir protobuf && tar -xf protobuf.tar.gz -C protobuf --strip-components=1 \
    && rm protobuf.tar.gz \
    && ( \
        cd protobuf \
        && ./configure \
        && make -j$(nproc) \
        && make install \
        && ldconfig \
        ) \
    && rm -rf protobuf

RUN mkdir grpc && tar -xf grpc.tar.gz -C grpc --strip-components=1 \
    && rm grpc.tar.gz \ 
    && ( \
        cd grpc \
        && make grpc_php_plugin \
       )

COPY ./go.tar.gz /go.tar.gz

ENV GOROOT=/go GOPATH=/godir PATH=$PATH:/go/bin:/godir/bin

RUN mkdir go && tar -xf go.tar.gz -C go --strip-components=1 \
    && go get -u github.com/golang/protobuf/protoc-gen-go \
    && rm go.tar.gz
