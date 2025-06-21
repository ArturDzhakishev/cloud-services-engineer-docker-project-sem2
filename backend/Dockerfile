# Этап 1 сборка
FROM golang:1.21-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN go build -o app ./cmd/api

# Этап 2 создание минимального образа
FROM alpine:latest

WORKDIR /app

COPY --from=builder /app/app .

EXPOSE 8081

CMD [ "./app" ]