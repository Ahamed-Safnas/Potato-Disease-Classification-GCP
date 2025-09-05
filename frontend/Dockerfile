# # Build stage
# FROM node:20-alpine AS build
# WORKDIR /app
# COPY package*.json ./
# # Use legacy OpenSSL if needed
# ENV NODE_OPTIONS=--openssl-legacy-provider
# RUN npm install
# COPY . .
# RUN npm run build

# # Production stage
# FROM nginx:alpine
# COPY --from=build /app/build /usr/share/nginx/html
# EXPOSE 80
# CMD ["nginx", "-g", "daemon off;"]

# Build stage
FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
# Use legacy OpenSSL if needed
ENV NODE_OPTIONS=--openssl-legacy-provider
RUN npm install
COPY . .
RUN npm run build

# Production stage
FROM nginx:alpine

# Copy build files
COPY --from=build /app/build /usr/share/nginx/html

# Force Nginx to use 8080 instead of 80
RUN sed -i "s/listen       80;/listen       8080;/" /etc/nginx/conf.d/default.conf

EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]
