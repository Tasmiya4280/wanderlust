# ------------------- Stage 1: Build Stage ------------------------------
FROM node:21 AS frontend-builder

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

# Copy env file before build so VITE_ variables are baked in
COPY .env.docker .env.local

# Build static files
RUN npm run build

# ------------------- Stage 2: Final Stage ------------------------------
FROM nginx:alpine

# Copy built static files to nginx
COPY --from=frontend-builder /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]