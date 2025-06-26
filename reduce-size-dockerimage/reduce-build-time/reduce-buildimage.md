In order to install the requirements for a Python project, all we need is a requirements.txt file.
What we can do to improve the build process is to copy this single file first and run pip install before copying the rest of the application code. This helps to avoid layer invalidation.



We should do the same for OS dependencies. Let’s move the RUN apt-get command before the COPY requirements.txt step

If we look at the rebuild time (the time required to rebuild the image after making a change in the application code)

Default: 38  seconds on average
Optimised:13.8 seconds on average 

 docker images
django-reduce-buildtime   latest    c5a6e4606ed2   9 seconds ago   1.11GB
simpledjango              latest    b3da05667e40   2 minutes ago   1.11GB
