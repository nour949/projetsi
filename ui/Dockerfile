# Use the official Nginx image
FROM nginx:latest

# Copy the Nginx configuration for frontend
COPY ./front.conf /etc/nginx/conf.d/default.conf

# Copy the frontend files to the appropriate location
COPY ./ /usr/share/nginx/html/

# Expose port 80 for HTTP
EXPOSE 80