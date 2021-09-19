FROM golang:buster
WORKDIR /server

COPY . .
RUN go mod vendor
RUN go build -o app main.go
EXPOSE 8080
CMD ./app