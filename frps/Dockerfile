FROM alpine

RUN apk add --no-cache wget bash \
    && cd / \
    && mkdir frps \
    && cd /tmp \
    && wget https://github.com/fatedier/frp/releases/download/v0.16.0/frp_0.16.0_linux_amd64.tar.gz \
    && tar -zxf frp_0.16.0_linux_amd64.tar.gz \
    && cd frp_0.16.0_linux_amd64 \
    && ls \
    && mv frps /frps/ \
    && mv frps.ini /frps/
    
ENTRYPOINT ["/frps/frps", "-c", "/frps/frps.ini"]
