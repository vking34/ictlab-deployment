FROM node:10.15.2 AS builder

WORKDIR /ictlab-frontend

# Copy source code
# Note: In COPY command, the destination starts from root
COPY . /ictlab-frontend

# Install app dependencies
RUN ls -la
RUN npm install

# Build production app
RUN npm run build

# Wrap web app with nginx
FROM nginx:1.17.10-alpine
COPY --from=builder /ictlab-frontend/build /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
