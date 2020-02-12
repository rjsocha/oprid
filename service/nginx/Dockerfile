FROM nginx:1.16-alpine
COPY common/tini-muslc-amd64 /sbin/tini
RUN apk --no-cache add inotify-tools bash socat
COPY nginx/oprid-nginx-manager /oprid-nginx-manager
RUN chmod +x /sbin/tini /oprid-nginx-manager
# This is cosmetic only
RUN deluser xfs \
    && delgroup www-data \
    && addgroup -g 33 -S www-data \
    && adduser -S -s /sbin/nologin -h /www -u 33 -G www-data -H -D www-data
COPY nginx/default.conf /etc/nginx/conf.d/
VOLUME /bus
ENTRYPOINT ["/sbin/tini", "--"]
CMD ["/oprid-nginx-manager"]
