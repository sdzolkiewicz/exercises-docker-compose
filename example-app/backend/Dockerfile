# use here COPY 1_13 .

FROM golang:trixie

EXPOSE 8080

WORKDIR /usr/src/app

COPY . .

ENV REQUEST_ORIGIN="http://localhost:8000"

RUN go build

CMD ["./server"]