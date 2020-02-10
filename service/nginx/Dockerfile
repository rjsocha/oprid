FROM nginx:1.16-alpine
COPY tini-muslc-amd64 /sbin/tini
RUN chmod +x /sbin/tini
RUN apk --no-cache add inotify-tools bash
COPY template/ /template/
COPY opird-nginx-watcher /sbin/opird-nginx-watcher
ENTRYPOINT ["/sbin/tini", "--"]
CMD ["/sbin/opird-nginx-watcher"]
