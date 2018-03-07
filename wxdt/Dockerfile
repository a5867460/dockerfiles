FROM ubuntu:16.04

ENV TZ=Asia/Shanghai

RUN apt-get install software-properties-common python-software-properties \
    add-apt-repository ppa:wine/wine-builds \
    dpkg --add-architecture i386 \
    apt-get update 

RUN apt-get install -y tzdata ca-certificates httpie git aptitude\
    aptitude search wine \
    apt-get install -y wine \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone \
    cd / \
    mkdir wxdt \
    cd wxdt \
    git clone https://github.com/cytle/wechat_web_devtools.git \
    cd wechat_web_devtools \
    ./bin/update_package_nw.s \
