FROM alpine as builder

ENV exporter_version 0.18.1

RUN apk update && apk upgrade && \
    apk add --no-cache bash curl

RUN curl -LO https://github.com/prometheus/node_exporter/releases/download/v${exporter_version}/node_exporter-${exporter_version}.linux-amd64.tar.gz \
    && tar -xvzf node_exporter-${exporter_version}.linux-amd64.tar.gz  \
    && cp node_exporter-${exporter_version}.linux-amd64/node_exporter /tmp/

FROM scratch

COPY --from=builder /tmp/node_exporter /usr/local/bin/

EXPOSE 9100

LABEL source=git@github.com:kyma-project/kyma.git

ENTRYPOINT ["node_exporter"]
