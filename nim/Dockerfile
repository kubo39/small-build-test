FROM alpine:latest AS builder

RUN apk add --no-cache nim gcc musl-dev

COPY main.nim .
RUN nim c --opt:size --threads:off --mm:arc --d:release -d:useMalloc --d:lto --d:strip -d:danger -d:noSignalhandler --panics:on --exceptions:quirky --passC:-fno-asynchronous-unwind-tables --passC:-ffunction-sections --passC:-fdata-sections --passL:-Wl,--build-id=none --passL:-Wl,--gc-sections --passL:-no-pie --passL:-static -o:hello main.nim

FROM scratch
COPY --from=builder /hello /hello
CMD ["/hello"]
