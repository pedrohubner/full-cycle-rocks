# full-cycle-rocks

FullCycle's Docker challenge — a minimal Go application containerized with a multi-stage Docker build, producing an ultra-small image based on `scratch`.

## What it does

Prints `Full Cycle Rocks!!` to stdout and exits.

## Requirements

- [Docker](https://www.docker.com/)

## Build

```bash
docker build -t full-cycle-rocks:1.0.0 .
```

## Run

```bash
docker run --name full-cycle-challenge full-cycle-rocks:1.0.0
```

## How the image is built

The Dockerfile uses a two-stage build:

1. **Builder** — compiles the Go binary inside `golang:1.24-alpine` with CGO disabled and stripped symbols (`-ldflags="-s -w"`), resulting in a static binary.
2. **Final** — copies only the binary into a `scratch` (empty) image, keeping the final image as small as possible.
