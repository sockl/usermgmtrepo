# use official node image as the base image
# using alpine version to reduce the image size
# build stage
FROM node:20-alpine AS build

# set the working directory inside the container
WORKDIR /app

# copy package.json and package-lock.json to the working directory
COPY package*.json ./

# install dependencies
RUN npm install

# copy the rest of the application code to the working directory
COPY . .

# build the react app for production
RUN npm run build

# static files will be generated in the /app/dist directory

# production stage
# serve the app with nginx server
# why nginx?
# nginx is a lightweight web server that can serve static files efficiently
FROM nginx:alpine

# copy the built react app from the build stage to the nginx html directory
COPY --from=build /app/dist /usr/share/nginx/html

# expose port 80 to the outside world
# when using nginx, the default port is 80
EXPOSE 80

# start nginx server
CMD ["nginx", "-g", "daemon off;"]