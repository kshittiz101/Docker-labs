# Use lightweight Alpine Linux version of Nginx (only ~5MB)
FROM nginx:alpine

# Set maintainer label (good for documentation)
LABEL maintainer="chaudharykshittiz950@gmail.com"
LABEL description="Static traveling website with Nginx base image"

# Remove default nginx welcome page (optional, keeps things clean)
RUN rm -rf /usr/share/nginx/html/*

# Copy custom HTML file to nginx web root
# Using COPY . . is better if you have multiple files
COPY index.html /usr/share/nginx/html/

# Copy custom nginx config (if you have one)
# COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80 (documentation purposes)
EXPOSE 80

# Nginx will start automatically (CMD is inherited from base image)
# The base nginx image already has: CMD ["nginx", "-g", "daemon off;"]