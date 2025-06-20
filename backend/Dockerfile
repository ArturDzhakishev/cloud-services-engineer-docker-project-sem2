FROM golang:alp

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN go build -o app

EXPOSE 8081

CMD [ "./app" ]