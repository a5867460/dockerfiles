FROM nginx:1.13-alpine

ENV TZ=Asia/Shanghai

RUN apt update && apt install -y tzdata \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone
