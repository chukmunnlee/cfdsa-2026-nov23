# first line is always the runtime time
FROM node:26-bookworm

## Define how to build the application
# Create a directory for my app 
# mkdir /app
WORKDIR /app

# below is in /app
COPY package.json .
COPY package-lock.json .
COPY main.js .
COPY public public
COPY views views

# Reinstall the dependencies
# /app/node_modules
RUN npm install
# We have installed the dependencies

## How to run the application
ENV APP_PORT="3000" 

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
   CMD curl -s -f http://localhost:${APP_PORT}/health > /dev/null || exit 1

# What ports the container need to open
EXPOSE ${APP_PORT} 

# defining a mount point
VOLUME /app/node_modules

# Specify the shell to run this
SHELL [ "/bin/sh", "-c" ]
# Command to run the app
ENTRYPOINT node main.js
