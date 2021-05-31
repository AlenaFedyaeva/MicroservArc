FROM golang:alpine as builder


# Set the Current Working Directory inside the container
WORKDIR /golang
# Copy everything from the current directory to the PWD (Present Working Directory) inside the container
COPY . .


# Download all the dependencies
RUN go get -d -v ./...

# Install the package
RUN go install -v ./...


RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o server .


FROM scratch

COPY --from=builder /golang/server /

EXPOSE 8080
CMD ["/server"]
