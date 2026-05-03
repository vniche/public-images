FROM node:24-trixie-slim AS build
ARG OS_ARCH="aarch64"

RUN npm install -g @mariozechner/pi-coding-agent \
    && pi install npm:pi-mcp-adapter \
    && npm cache clean --force

USER node

WORKDIR /home/node

CMD ["pi"]