# Use the official Node.js image as a build environment
FROM node:alpine AS build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Use the official nginx image to serve the static files
FROM nginx:alpine

# Copy the build output from the previous stage
COPY --from=build /app/build /usr/share/nginx/html

# Expose the port nginx is serving on
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
