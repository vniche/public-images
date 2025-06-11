FROM python:3.12

WORKDIR /app

ADD https://github.com/basicmachines-co/basic-memory/releases/download/v0.13.0/basic_memory-0.13.0.tar.gz .

RUN tar -xzf basic_memory-0.13.0.tar.gz \
    && mv basic_memory-0.13.0/* ./ \
    && rm -rf basic_memory-0.13.0/

RUN pip install -e .

CMD ["basic-memory", "mcp", "--transport", "streamable-http"]