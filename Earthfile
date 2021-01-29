FROM alpine:3.11

build-env:
    RUN apk add --no-cache gcc musl-dev wget && \
        wget https://nim-lang.org/download/nim-1.4.2-linux_x64.tar.xz && \
        tar -xvf nim-1.4.2-linux_x64.tar.xz
    ENV PATH "${PATH}:/nim-1.4.2/bin"
    RUN nimble refresh

deps:
    FROM +build-env
    RUN apk add --no-cache git
    RUN mkdir -p /src/serv
    COPY src /src/serv/src
    COPY serv.nimble /src/serv
    WORKDIR /src/serv
    RUN nimble build  --passL:-static
    SAVE ARTIFACT serv AS LOCAL serv

