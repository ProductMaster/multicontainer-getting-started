FROM arm32v6/alpine:latest


RUN apk add --update tzdata
ENV TZ=Asia/Shanghai

ENV VERSION 0.29.0
ENV PLATFORM arm64

WORKDIR /home/root/

RUN wget https://github.com/fatedier/frp/releases/download/v0.29.0/frp_0.29.0_linux_arm64.tar.gz
RUN mv frp_0.29.0_linux_arm64.tar.gz frp.tar.gz

#COPY frp.tar.gz .

RUN mkdir frp && \
    tar -zvxf frp.tar.gz \
    && rm -rf frp_${VERSION}_linux_${PLATFORM}/system* \
    && cp frp_${VERSION}_linux_${PLATFORM}/* ./frp \
    && rm -rf frp_${VERSION}_linux_*

# Clean APK cache
RUN rm -rf /var/cache/apk/*

#RUN mkdir /conf
#VOLUME /conf

COPY frpc.ini /frpc.ini

WORKDIR /home/root/frp/

CMD ["./frpc","-c","/frpc.ini"]
