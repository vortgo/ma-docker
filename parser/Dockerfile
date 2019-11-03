FROM golang:1.12.0-alpine3.9 AS builder

RUN mkdir /app
WORKDIR /app
RUN apk add --update --no-cache git
RUN git clone https://github.com/vortgo/ma-parser ./

ARG COMMIT=${COMMIT}
RUN git checkout ${COMMIT}

RUN go mod download
RUN go build -o main .

# final stage
FROM alpine:latest
RUN apk --no-cache add ca-certificates
COPY --from=builder /app/main ./
RUN chmod +x ./main
ENTRYPOINT ["./main"]
