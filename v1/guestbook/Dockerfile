# Stage 1: Build the Go application
FROM golang:1.18 as builder

WORKDIR /app

COPY main.go .

RUN go mod init guestbook
RUN go mod tidy

RUN go build -o main main.go

# Stage 2: Create the runtime image
FROM ubuntu:18.04

# Copy the built Go binary from the builder stage
COPY --from=builder /app/main /app/guestbook

# Add static files to the runtime image
ADD public/index.html /app/public/index.html
ADD public/script.js /app/public/script.js
ADD public/style.css /app/public/style.css
ADD public/jquery.min.js /app/public/jquery.min.js

# Set the working directory
WORKDIR /app

# Expose the application port
EXPOSE 3000

# Define the default command to run the application
CMD ["./guestbook"]
