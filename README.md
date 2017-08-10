# HUGO Website Engine in Docker

**Dockerized version of the HUGO (gohugo.io) executable. This is forked from [giantswarm](https://github.com/giantswarm/hugo-docker), the only differences are:**

1. the addition of asciidoctor
2. updated alpine version
3. updated hugo version and modifying the commands to accommodate**

More about Hugo: http://www.gohugo.io/

The below "Running" documentation has only been slightly modified from original and is great information.  However, for my use, I really only need to run the hugo server on a preexisting project/site:

```
docker run --rm -d -v $(pwd):$(pwd):z  -w $(pwd) \
           -p 1313:1313 --name hugo \
           dswhitley/hugo server --bind=0.0.0.0
```

And now, I can browse to http://localhost:1313 and see the changes I make to my site in realtime.

----

## Running

This is a simplistic example of how to call the hugo executable:

    docker run --rm -ti dswhitley/hugo help

To make it really useful, you'll need to mount the current directory to the container, so hugo can write files:

    docker run --rm -ti -v $(pwd):$(pwd) -w $(pwd) dswhitley/hugo new site ./site

To make the command a bit more accessible, create an alias. Note that we add the `-p` option here to make hugo's HTTP port 1313 available.

    alias myhugo="docker run --rm -ti -v $(pwd):$(pwd) -w $(pwd) -p 1313:1313 dswhitley/hugo"

Then we can call hugo like this:

    # Creating a new site in folder ./site
    myhugo new site ./site

    # Serve using hugo's built-in server
    # (use your currect Docker IP address in the baseUrl)
    myhugo server --theme=hyde --baseUrl=http://192.168.59.103 --bind=0.0.0.0 -s ./site

    # Generate public files and exit
    myhugo --theme=hyde --baseUrl=http://192.168.59.103 -s ./site

## Build your own

To build your own image, do this:

    docker build -t dswhitley/hugo .
