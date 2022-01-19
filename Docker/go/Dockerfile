##### Stage 1 #####

### Use golang:1.15 as base image for building the application
FROM golang:1.17 as builder

WORKDIR /go/src

COPY fullcycle-rocks.go .

### CGO has to be disabled cross platform builds
### Otherwise the application won't be able to start
ENV CGO_ENABLED=0

### Build the Go app for a linux OS
### 'scratch' and 'alpine' both are Linux distributions
RUN GOOS=linux go build fullcycle-rocks.go && \
    rm fullcycle-rocks.go

##### Stage 2 #####

### Define the running image
FROM scratch

### Set working directory
WORKDIR /app

### Copy built binary application from 'builder' image
COPY --from=builder /go/src/ .

ENTRYPOINT ["/app/fullcycle-rocks"]
