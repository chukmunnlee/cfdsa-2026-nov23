# build container
FROM golang:1.27-bookworm AS builder

WORKDIR /src

COPY go.* .
COPY main.go .

# /src/app
RUN CGO_ENABLED=0 go build -o app .
# get a binary file app

# run container
FROM debian:bookworm

WORKDIR /app

COPY public public
COPY templates templates
COPY --from=builder /src/app .

ENV PORT="3000" INSTANCE_NAME="dov-bear" INSTANCE_HASH=""

EXPOSE ${PORT}

SHELL [ "/bin/sh", "-c" ]
ENTRYPOINT ./app