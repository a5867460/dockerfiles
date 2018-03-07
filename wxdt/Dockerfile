FROM ubuntu:16.04

ENV TZ=Asia/Shanghai \
    WINEARCH=win32 WINEPREFIX=~/.wine32 winecfg

RUN sudo apt update \
    sudo apt install -y tzdata ca-certificates httpie wine \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone \
    cd / \
    mkdir wxdt \
    cd wxdt \
    git clone git@github.com:cytle/wechat_web_devtools.git \
    cd wechat_web_devtools \
    ./bin/update_package_nw.s \
