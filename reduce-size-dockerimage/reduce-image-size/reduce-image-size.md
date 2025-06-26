There are a few ways to reduce the size of a Docker image without impacting its functionality. Smaller sizes mean quicker uploads and downloads, and quicker uploads and downloads result in faster CI/CD processes or other scripts.

Our Docker image currently have 1.16GB, let’s reduce that.

➜  ~ docker images | grep docker-opt
docker-opt-tutorial  latest  a171d964a545  10 seconds ago  1.16GB

Base image
A great place to start would be to review our base image. The default Python images use Debian distributions, but there are more lightweight alternatives available on Docker Hub.

A better choice here would be to use the Alpine version of the image, such as python:3.10-alpine, which is significantly smaller and more secure as it uses Linux Alpine.

Before proceeding, you need to ensure that the OS libraries you install are compatible with this distribution.

Replace the base image definition accordingly.

FROM python:3.10-alpine
Alpine uses apk instead of apt-get

# Install os dependencies
RUN apk add --no-cache vim
