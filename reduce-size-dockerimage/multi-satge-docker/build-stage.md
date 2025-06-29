Docker build stages, also known as multi-stage builds, separate the build process into distinct stages, such as a “builder” stage for compiling or installing dependencies, and a “runtime” stage for the final, lean image. This approach ensures that only the essential runtime files are included in the final image, reducing size and improving performance.


1. Added as builder to the base image command: This allows us to reference this stage in other parts of the Dockerfile.
2. Kept installing dependencies in the builder stage: In the builder stage, we handle installing dependencies. While vim is just an example, it’s common to install additional libraries needed only for dependency installation, which may not be required during runtime.
3. Added a second FROM python:3.10-alpine command: This indicates a new stage in the Dockerfile. In this stage, we skip re-installing dependencies.
4. Used COPY --from=builder /root/.local /root/.local: This copies /root/.local from the builder stage to the runtime stage, ensuring that only the necessary files are included in the final image.
5.Added ENV PATH="/root/.local/bin:$PATH": This ensures that tools copied from the builder stage are available in the runtime stage.


REPOSITORY                TAG       IMAGE ID       CREATED          SIZE
django-multistage-build   latest    b190dfd8667b   13 seconds ago   83.3MB
django-reduce-imagesize   latest    7b4c584eb2c9   2 minutes ago    132MB
django-reduce-buildtime   latest    c5a6e4606ed2   5 minutes ago    1.11GB
simpledjango              latest    b3da05667e40   8 minutes ago    1.11GB


![Untitled (2)](https://github.com/user-attachments/assets/4477051a-dddd-4c5b-860b-8fb838d50dc4)


Exclude files from build
Docker allows us to create a .dockerignore file to ensure that certain files are not included in the image by mistake, such as the local development database, environment variable files, or the .venv directory when running COPY . .

Here’s an example of a simple .dockerignore file to include in the root of your project

# .dockerignore
.venv


