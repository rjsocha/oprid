FROM alpine
COPY common/tini-muslc-amd64 /sbin/tini
RUN apk --no-cache add dnsmasq unbound socat
COPY dns/unbound.conf /etc/unbound/unbound.conf
COPY dns/dnsmasq.conf /etc/dnsmasq.conf
COPY dns/opird-dns-manager /sbin/opird-dns-manager
RUN chmod +x /sbin/tini /sbin/opird-dns-manager 
VOLUME /bus
ENTRYPOINT ["/sbin/tini", "--"]
CMD ["/sbin/opird-dns-manager"]
