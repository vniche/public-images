FROM python:3.12-slim AS build-env

ARG BASIC_MEMORY_VERSION=0.13.0

WORKDIR /app

ADD https://github.com/basicmachines-co/basic-memory/releases/download/v${BASIC_MEMORY_VERSION}/basic_memory-${BASIC_MEMORY_VERSION}.tar.gz .

RUN tar -xzf basic_memory-${BASIC_MEMORY_VERSION}.tar.gz && \
    mv basic_memory-${BASIC_MEMORY_VERSION}/* ./ && \
    rm -rf basic_memory-${BASIC_MEMORY_VERSION}/

RUN pip install -e .

FROM gcr.io/distroless/python3:nonroot

ENV PYTHONPATH=/usr/local/lib/python3.12/site-packages
ENV PATH=/usr/local/bin:$PATH

COPY --from=build-env /usr/local/lib/python3.12/site-packages /usr/local/lib/python3.12/site-packages
COPY --from=build-env /usr/local/bin /usr/local/bin
COPY --from=build-env /usr/local/lib /usr/local/lib
COPY --from=build-env /app /app

ENTRYPOINT ["basic-memory"]

CMD ["mcp", "--transport", "streamable-http"]
