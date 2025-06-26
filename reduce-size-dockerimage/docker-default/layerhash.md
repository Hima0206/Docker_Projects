It’s important to understand that Docker images consist of layers, with each layer being built based on the previous one, starting from the top of the Dockerfile and proceeding downward. This means we should place operations that are less likely to change closer to the top or beginning of the file.

In our example, any code change will be included in the COPY . . command, changing its hash. This, in turn, will invalidate any layer that comes after it. The result? Package installation will run again, even if none of the requirements have changed.
