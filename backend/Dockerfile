# Этап 1 сборка
FROM golang:1.21-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN go build -o app ./cmd/api

# Этап 2 создание минимального образа
FROM alpine:latest

RUN apk add --no-cache curl

RUN addgroup -S backendgroup && adduser -S appuser -G backendgroup

WORKDIR /app

COPY --from=builder /app/app .

RUN chown -R appuser:backendgroup /app

USER appuser 

EXPOSE 8081

CMD [ "./app" ]