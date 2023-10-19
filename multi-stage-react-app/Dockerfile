FROM node:lts-alpine AS build
WORKDIR /usr/local/app

# Install React build dependencies
COPY package.json yarn.lock ./
RUN yarn install && yarn cache clean

# Copy in the rest of the config and the application content
COPY . .
# Note ignore the Dockerfile / README.md in dockerignore file

# Perform the build itself, which drops the assets at /usr/local/app/dist
RUN yarn build

# TODO - Create a new stage that copies the built assets into the webroot of an nginx:alpine image
#FROM nginx:1.25.2-alpine3.18-slim
FROM nginx:alpine
COPY --from=build /usr/local/app/dist /usr/share/nginx/html
#EXPOSE 8085
CMD ["nginx", "-g", "daemon off;"]