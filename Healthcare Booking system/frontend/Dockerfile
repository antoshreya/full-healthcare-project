# frontend/Dockerfile

# ---- Stage 1: Build ----
# Use a Node.js image to build the project
FROM node:18-alpine AS builder

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the frontend source code
COPY . .

# Build the app for production
RUN npm run build

# ---- Stage 2: Serve ----
# Use a lightweight Nginx image to serve the static files
FROM nginx:stable-alpine

# Copy the built files from the 'builder' stage
COPY --from=builder /app/dist /usr/share/nginx/html

# Expose port 80 for the Nginx server
EXPOSE 80

# The default Nginx command will start the server
CMD ["nginx", "-g", "daemon off;"]