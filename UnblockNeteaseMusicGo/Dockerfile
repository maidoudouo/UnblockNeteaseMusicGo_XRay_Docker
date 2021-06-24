FROM golang:1.16.5 as builder

LABEL maintainer="maidoudouo <maidoudouo@outlook.com>"
LABEL stage=builder

RUN sed -i 's#http://deb.debian.org#https://mirrors.ustc.edu.cn#g' /etc/apt/sources.list
RUN sed -i 's|security.debian.org/debian-security|mirrors.ustc.edu.cn/debian-security|g' /etc/apt/sources.list
RUN apt-get update
RUN apt-get install git -y
RUN git clone https://github.com/cnsilvan/UnblockNeteaseMusic /UnblockNeteaseMusic
WORKDIR /UnblockNeteaseMusic
RUN chmod 755 build.sh
RUN ./build.sh

FROM ubuntu
LABEL maintainer="maidoudouo <maidoudouo@outlook.com>"
COPY --from=builder /UnblockNeteaseMusic/bin/UnblockNeteaseMusic /usr/local/bin/UnblockNeteaseMusic
RUN chmod +x /usr/local/bin/UnblockNeteaseMusic

COPY entrypoint.sh /usr/local/bin/
ENTRYPOINT ["entrypoint.sh"]