FROM alpine
COPY common/tini-muslc-amd64 /sbin/tini
RUN apk --no-cache add inotify-tools bash socat findutils
COPY manager/template/ /template/
COPY manager/opird-manager /opird-manager
RUN chmod +x /sbin/tini /opird-manager
# This is cosmetic only
RUN deluser xfs \
    && addgroup -g 33 -S www-data \
    && adduser -S -s /sbin/nologin -h /www -u 33 -G www-data -H -D www-data
VOLUME /bus
ENTRYPOINT ["/sbin/tini", "--"]
CMD ["/opird-manager"]
