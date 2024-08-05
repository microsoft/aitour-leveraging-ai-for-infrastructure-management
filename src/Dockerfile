# Stage 1: Build the Go application
FROM golang:bullseye AS build

# Create a non-root user
RUN useradd -u 10001 -m nonroot

# Set the working directory inside the container
WORKDIR /app

# Copy go.mod and go.sum files
COPY go.mod ./

# Download dependencies
RUN go mod download

# Copy the rest of the application code
COPY . .

# Build the Go application binary
# RUN go build -o go-web-app
RUN go build \
    -ldflags="-linkmode external -extldflags -static" \
    -tags netgo \
    -o go-web-app

# CMD ["./go-web-app"]

# Use a minimal scratch image as the base
FROM scratch

# Copy /etc/passwd for non-root user information
COPY --from=build /etc/passwd /etc/passwd

# Copy the compiled application binary
COPY --from=build /app/go-web-app /go-web-app

# Use the non-root user
USER nonroot

# Expose the application port
EXPOSE 8080

# Define the command to run the application
CMD ["./go-web-app"]