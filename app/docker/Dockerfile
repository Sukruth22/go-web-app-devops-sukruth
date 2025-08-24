# --- build stage ---
FROM golang:1.22 AS build
WORKDIR /src
COPY app/go.mod app/go.sum ./
RUN go mod download
COPY app/ .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o /out/app ./...

# --- run stage ---
FROM gcr.io/distroless/static:nonroot
WORKDIR /app
COPY --from=build /out/app /app/app
USER nonroot:nonroot
EXPOSE 8080
ENTRYPOINT ["/app/app"]
