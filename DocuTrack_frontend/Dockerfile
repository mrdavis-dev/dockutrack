# Dockerfile para DocuTrack Frontend (React + Vite)
FROM node:20-alpine AS build

WORKDIR /app

COPY package.json package-lock.json* ./
RUN npm install

COPY . .
RUN npm run build

# Servir con un servidor web estático
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html

# Copia configuración personalizada de nginx si existe
# COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
