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

RUN docker-php-ext-install -j$(nproc) bcmath \
    && docker-php-ext-install pdo_mysql \
    && wget https://github.com/grpc/grpc/archive/v1.20.1.tar.gz -O grpc.tar.gz \
    && wget https://github.com/protocolbuffers/protobuf/releases/download/v3.7.1/protobuf-all-3.7.1.tar.gz -O protobuf.tar.gz \
    && wget https://dl.google.com/go/go1.12.4.linux-amd64.tar.gz -O go.tar.gz

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

ENV GOROOT=/go GOPATH=/godir PATH=$PATH:/go/bin:/godir/bin

RUN mkdir go && tar -xf go.tar.gz -C go --strip-components=1 \
    && go get -u github.com/golang/protobuf/protoc-gen-go \
    && rm go.tar.gz
