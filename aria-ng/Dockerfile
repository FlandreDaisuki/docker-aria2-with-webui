FROM alpine:3.19

ARG ARIA_NG_VERSION=1.3.7

RUN mkdir -p /conf \
	&& mkdir -p /conf-copy \
	&& mkdir -p /data \
	&& apk add --no-cache tzdata aria2 darkhttpd s6

RUN apk add --no-cache --virtual .install-deps curl unzip \
	&& mkdir -p /aria2-ng \
	&& curl -o /aria2-ng.zip -L "https://github.com/mayswind/AriaNg/releases/download/${ARIA_NG_VERSION}/AriaNg-${ARIA_NG_VERSION}-AllInOne.zip" \
	&& unzip /aria2-ng.zip -d /aria2-ng \
	&& rm /aria2-ng.zip \
	&& apk del .install-deps

COPY files/start.sh /conf-copy/start.sh
COPY files/aria2.conf /conf-copy/aria2.conf

RUN chmod +x /conf-copy/start.sh

WORKDIR /

VOLUME ["/data"]
VOLUME ["/conf"]

EXPOSE 6800
EXPOSE 80

CMD ["/conf-copy/start.sh"]
