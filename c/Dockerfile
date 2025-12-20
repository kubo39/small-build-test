FROM alpine:latest AS builder

RUN apk add --no-cache build-base musl-dev

COPY main.c .
RUN gcc -fno-asynchronous-unwind-tables -ffunction-sections -fdata-sections -Wl,--gc-sections -Wl,--build-id=none -static -Os -no-pie -z norelro -s -o hello main.c

FROM scratch
COPY --from=builder /hello /hello
CMD ["/hello"]
