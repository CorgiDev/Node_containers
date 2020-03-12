# Node.js 13.10.1
This is the UBI8 base image with Nodejs, NPM, Nodemon, and NSS_wrapper. This version uses a tar.gz file to build 13.10.1 Node.js and NPM. Nodemon and NSS_wrapper are installed using RPMs.

## Ports
To effectively run this container requires port 8080 be exposed.

## Running the Container
In order to run the container:

`docker run --name nodejs12 -it -p 8080:8080/tcp name:tag /bin/bash`

Replace the container *name:tag* with the name/tag of your copy of the container.
You can also swap out the *--name* for something other than nodejs if needed.

## Resource Requirements
This container is meant to act as a base. As a result, resource requirements will depend on the downstream container.

## Vendor Documentation
- [Node.js 13.X LTS Documentation](https://nodejs.org/docs/latest-v13.x/api/modules.html)

## Note
- No user account is included in this container to avoid conflicts with downstream applications that run on top of it. As a result,it will be dependent on downstream containers to avoid running as root.
- Some Nodejs applications may require nodemon or nss_wrapper to be added to this image. You can add these to `ARG INSTALL_PKGS` if you need to include them. 
  - However, this may introduce additional vulnerabilities unless they are updated to the latest versions online.