# Build Stage
# First pull Golang image
FROM golang:1.17-alpine as build-env

# Set environment variable
ENV APP_NAME warden
ENV CMD_PATH main.go

# Copy application data into image
COPY ./warden $GOPATH/src/$APP_NAME
COPY go.mod $GOPATH/src/$APP_NAME
COPY go.sum $GOPATH/src/$APP_NAME

WORKDIR $GOPATH/src/$APP_NAME

# Budild application
RUN CGO_ENABLED=0 go build -v -o /$APP_NAME $GOPATH/src/$APP_NAME/$CMD_PATH

# Run Stage
FROM alpine:3.14

# Set environment variable
ENV APP_NAME warden

# Copy only required data into this image
COPY --from=build-env /$APP_NAME .

# Start app
CMD ./$APP_NAME
