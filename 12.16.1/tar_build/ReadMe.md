# Node.js 12.16.1
This is the UBI8 base image with Nodejs, NPM, Nodemon, and NSS_wrapper. This version installs Nodejs and NPM using the official Node.js tar.gz file for version 12.16.1.

## Ports
To effectively run this container requires port 8080 be exposed.

## Running the Container
In order to run the container:

`docker run --name nodejs12 -it -p 8080:8080/tcp name:tag /bin/bash`

Replace the container *name:tag* with the name/tag of your copy of the container.
You can also swap out the *--name* for something other than nodejs if needed.

## Node.js Official Documentation
- [Node.js 12.X LTS Documentation](https://nodejs.org/docs/latest-v12.x/api/modules.html)