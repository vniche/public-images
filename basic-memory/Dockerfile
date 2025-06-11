FROM python:3.12

ARG BASIC_MEMORY_VERSION=0.13.0

WORKDIR /app

ADD https://github.com/basicmachines-co/basic-memory/releases/download/v${BASIC_MEMORY_VERSION}/basic_memory-${BASIC_MEMORY_VERSION}.tar.gz .

RUN tar -xzf basic_memory-${BASIC_MEMORY_VERSION}.tar.gz && \
    mv basic_memory-${BASIC_MEMORY_VERSION}/* ./ && \
    rm -rf basic_memory-${BASIC_MEMORY_VERSION}/

RUN pip install -e .

ENTRYPOINT ["basic-memory"]

CMD ["mcp", "--transport", "streamable-http"]
