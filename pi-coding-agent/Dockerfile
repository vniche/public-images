FROM node:24-trixie-slim AS build
ARG OS_ARCH="aarch64"

RUN npm install -g @mariozechner/pi-coding-agent

FROM gcr.io/distroless/nodejs24-debian13:nonroot

ARG OS_ARCH="aarch64"

# pi coding agent
COPY --from=build /usr/local/lib/node_modules/@mariozechner/pi-coding-agent /usr/local/lib/node_modules/@mariozechner/pi-coding-agent

# runtime dependencies
COPY --from=build /usr/bin/tar /usr/bin/date /usr/bin/mkdir /usr/bin/gzip /usr/bin/sleep /usr/bin/
COPY --from=build /bin/sh /bin/
COPY --from=build /lib/${OS_ARCH}-linux-gnu/libacl.so.1 /lib/${OS_ARCH}-linux-gnu/libselinux.so.1 /lib/${OS_ARCH}-linux-gnu/libpcre2-8.so.0 /lib/${OS_ARCH}-linux-gnu/

USER nonroot

WORKDIR /home/nonroot

RUN mkdir -p /home/nonroot/.pi/agent/{sessions,skills,bin}

CMD ["/usr/local/lib/node_modules/@mariozechner/pi-coding-agent/dist/cli.js"]