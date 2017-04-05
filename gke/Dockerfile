FROM nginx:1.11.9-alpine
MAINTAINER mnuma

RUN apk --update add --no-cache tzdata && \
    cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && \
    apk del tzdata && \
    rm -rf /var/cache/apk/*

EXPOSE 443
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
