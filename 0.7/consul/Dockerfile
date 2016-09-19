FROM alpine:3.2

ENV CONSUL_VERSION 0.7.0
ENV CONSUL_SHA256 b350591af10d7d23514ebaa0565638539900cdb3aaa048f077217c4c46653dd8
ENV GLIBC_VERSION "2.23-r1"

RUN apk --update add curl ca-certificates && \
    curl -Ls https://github.com/andyshinn/alpine-pkg-glibc/releases/download/${GLIBC_VERSION}/glibc-${GLIBC_VERSION}.apk > /tmp/glibc-${GLIBC_VERSION}.apk && \
    apk add --allow-untrusted /tmp/glibc-${GLIBC_VERSION}.apk && \
    rm -rf /tmp/glibc-${GLIBC_VERSION}.apk /var/cache/apk/*
ADD https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip /tmp/consul.zip
RUN echo "${CONSUL_SHA256}  /tmp/consul.zip" > /tmp/consul.sha256 \
  && sha256sum -c /tmp/consul.sha256 \
  && cd /bin \
  && unzip /tmp/consul.zip \
  && chmod +x /bin/consul \
  && rm /tmp/consul.zip

ENTRYPOINT ["/bin/consul"]
