#// the base image to use for building this Docker image. In this case, it's starting from the node:6-alpine image, which is a lightweight Alpine Linux-based image with Node.js version 6 installed.
FROM node:6-alpine 
#This line informs Docker that the container will listen on port 3000 at runtime
EXPOSE 3000
# tini is a tiny but powerful init system for containers. The --no-cache option is used to prevent apk from caching the index locally, saving space.
RUN apk add --no-cache tini
#This line sets the working directory inside the container
WORKDIR /usr/src/app
#copies the package.json file from the host machine to the /usr/src/app directory 
COPY package.json package.json
#runs npm install to install dependencies listed in the package.json file. The && operator is used to chain commands together, so npm cache clean --force will be executed if npm install completes successfully.
RUN npm install && npm cache clean --force
#This includes application source code, configuration files, and any other necessary files.
COPY . .
#This line specifies the command that will be executed when the container starts. It uses tini as the init system (/sbin/tini) to handle signal forwarding and then starts the Node.js application by running node ./bin/www. This assumes that ./bin/www is the entry point file for the Node.js application.
CMD [ "/sbin/tini", "--", "node", "./bin/www" ]