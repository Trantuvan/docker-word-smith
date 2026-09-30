# syntax=docker/dockerfile:1

FROM golang:1.27-alpine AS build

WORKDIR /app
RUN --mount=type=cache,target=/go/pkg/mod/ \
    --mount=type=bind,source=dispatcher.go,target=dispatcher.go \
    go build -o ./server ./dispatcher.go

FROM alpine:3.24

WORKDIR /app
EXPOSE 80
COPY static/ static/
COPY --from=build /app/server /app/
CMD [ "./server" ]