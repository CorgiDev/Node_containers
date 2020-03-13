# Node.js
This is the UBI8 base image with Nodejs and NPM.

## Ports
To effectively run this container requires port 8080 be exposed.

## Running the Container
In order to run the container:

`docker run --name nodejs12 -it -p 8080:8080/tcp name:tag /bin/bash`

Replace the container *name:tag* with the name/tag of your copy of the container.
You can also swap out the *--name* for something other than nodejs if needed.

## Documentation
- [Node.js 12.X LTS Documentation](https://nodejs.org/docs/latest-v12.x/api/modules.html)
- [Node.js 13.X LTS Documentation](https://nodejs.org/docs/latest-v13.x/api/modules.html)
- [NPM Documentation](https://docs.npmjs.com/)
- [npm update documentation](https://docs.npmjs.com/cli-commands/update.html)
  - I recommend looking over this because there are some different ways to use the `npm update` command that affect what it updates and how.

## Note
- This repo currently containers the following versions of Nodejs:
  - Nodejs 12.16.1 rpm build
  - Nodejs 12.16.1 tar build
  - Nodejs 13.10.1 tar build