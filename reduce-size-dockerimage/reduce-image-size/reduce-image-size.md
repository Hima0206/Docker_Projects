There are a few ways to reduce the size of a Docker image without impacting its functionality. Smaller sizes mean quicker uploads and downloads, and quicker uploads and downloads result in faster CI/CD processes or other scripts.

Our Docker image currently have 1.11GB, let’s reduce that.


Base image
A great place to start would be to review our base image. The default Python images use Debian distributions, but there are more lightweight alternatives available on Docker Hub.

A better choice here would be to use the Alpine version of the image, such as python:3.10-alpine, which is significantly smaller and more secure as it uses Linux Alpine.

Before proceeding, you need to ensure that the OS libraries you install are compatible with this distribution.

Replace the base image definition accordingly.

FROM python:3.10-alpine
Alpine uses apk instead of apt-get

# Install os dependencies
RUN apk add --no-cache vim


REPOSITORY                TAG       IMAGE ID       CREATED          SIZE
django-reduce-imagesize   latest    7b4c584eb2c9   10 seconds ago   132MB
django-reduce-buildtime   latest    c5a6e4606ed2   3 minutes ago    1.11GB
simpledjango              latest    b3da05667e40   5 minutes ago    1.11GB

