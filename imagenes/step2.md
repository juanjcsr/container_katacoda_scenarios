## Escribe el Dockerfile

<pre class="file" data-filename="Dockerfile" data-target="replace">
# Start with the scratch (empty) image
FROM scratch

# Copy the hello binary into the root directory
COPY hello /

# Copy the response text file into the location where the container expects it to be
COPY text/response /text/response

# Tell Docker what executable to run by default when starting this container
ENTRYPOINT ["/hello"]
</pre>

## Construye tu imagen

`docker build -t hello  .`{{execute}}

