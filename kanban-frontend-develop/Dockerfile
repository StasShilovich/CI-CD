# Stage 1: Build the Angular app
FROM node:10-alpine AS builder

# Set working directory
WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm install

# Copy all source files
COPY . .

# Build the Angular app
RUN ./node_modules/.bin/ng build --prod

# Stage 2: Serve the app with Nginx
FROM nginx:alpine

# Copy custom NGINX config
COPY default.conf /etc/nginx/conf.d/default.conf

# Copy built files from previous stage to Nginx html directory
COPY --from=builder /app/dist/kanban-ui /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start nginx server
CMD ["nginx", "-g", "daemon off;"]
