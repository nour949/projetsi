FROM nginx:latest

# Copy key & cert

COPY nginx.crt /etc/nginx/ssl/server.crt
COPY nginx.key /etc/nginx/ssl/server.key

# Copy Nginx configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf


EXPOSE 443