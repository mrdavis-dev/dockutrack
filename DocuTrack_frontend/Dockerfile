# Dockerfile - DocuTrack Frontend (React + Vite)
FROM node:20-alpine AS build
WORKDIR /app

# Mejor cache de dependencias
COPY package.json package-lock.json* ./
RUN npm ci || npm install

# Build de la app
COPY . .
RUN npm run build

# --- Etapa de runtime (Nginx) ---
FROM nginx:alpine
# Config Nginx: SPA fallback (+ proxy opcional a /api)
COPY nginx.conf /etc/nginx/nginx.conf
# Archivos estáticos
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
