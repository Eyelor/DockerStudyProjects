# docker-zadanie1-geoip-server-extended
This project showcases the process of building a Docker image with a server-side application that responds with the client's IP and time. It also uses Buildx with a custom builder to create images for many platforms at once while caching to different images.

## Table of Contents

- [Requirements](#requirements)
- [Image Building](#image-building)

## Requirements

For Linux and Windows systems Docker or Docker Desktop must be installed and running.

For Windows systems WSL must be installed.

Example for Windows:

To create a builder:

```cmd
docker buildx create --name zadanie1builder --driver docker-container --bootstrap
```

Result:

![Builder Build](screenshots/builder-build.jpg)

To use the created builder:

```cmd
docker buildx use zadanie1builder
```

Result:

![Builder Use](screenshots/builder-use.jpg)

To check if the builder is selected as default, open Docker Desktop > Settings > Builders.

Result:

![Builder Check](screenshots/builder-check.jpg)

## Image Building

Run the command below to build the image. Change the '-t' parameter value to your desired image repository  and tag on your account. Choose the platforms you want. Set a separate image for cache on your repository.

```cmd
docker buildx build -t docker.io/eyelor/zadanie1:geoip-server-extended --platform linux/amd64,linux/arm64 --push --cache-to=type=registry,ref=docker.io/eyelor/zadanie1:geoip-server-extended-cache --cache-from=type=registry,ref=docker.io/eyelor/zadanie1:geoip-server-extended-cache --builder zadanie1builder .
```

Result:

![Extended Push First](screenshots/extended-push-first.jpg)

Run the previous command again to see if the cache was used.

Result:

![Extended Push Cached](screenshots/extended-push-cached.jpg)

Red ERROR dissapeared meaning that the cache was used this time.

Link to these images: [hub.docker.com/r/eyelor/zadanie1/tags](https://hub.docker.com/r/eyelor/zadanie1/tags)

Documentation for the server app and Dockerfile here: [github.com/Eyelor/docker-zadanie1-geoip-server-basic/blob/main/zadanie1.md](https://github.com/Eyelor/docker-zadanie1-geoip-server-basic/blob/main/zadanie1.md)

