FROM golang:alpine AS builderDefault

RUN apk update && apk add --no-cache git
WORKDIR $GOPATH/src/codeeducation/app/
COPY src/. .

RUN go get -d -v

RUN GOOS=linux GOARCH=amd64 go build -ldflags="-w -s" -o /go/bin/main

FROM scratch

COPY --from=builderDefault /go/bin/main /go/bin/main

ENTRYPOINT ["/go/bin/main"]