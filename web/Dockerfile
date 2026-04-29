FROM golang:alpine AS builder

COPY dispatcher.go .
RUN go build dispatcher.go

FROM alpine

COPY --from=builder /go/dispatcher .
COPY static static

CMD ["./dispatcher"]
