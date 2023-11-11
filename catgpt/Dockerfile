ARG GOARCH=amd64
FROM golang:1.21-alpine as builder
WORKDIR /go/src/catgpt
COPY . .
RUN go mod download
RUN CGO_ENABLED=0 GOARCH=${GOARCH} go build -o /go/bin/catgpt

FROM gcr.io/distroless/base-debian12:latest-${GOARCH}
COPY --from=builder /go/bin/catgpt /
EXPOSE 8080 9090
CMD ["/catgpt"]