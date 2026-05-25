# ==========================================
# ETAPA 1: Construcción del Frontend
# ==========================================
FROM node:18-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm install
COPY . .
# Compila los archivos estáticos (HTML, JS, CSS)
RUN npm run build

# ==========================================
# ETAPA 2: Distribución Segura con Nginx
# ==========================================
# Usamos una imagen oficial de Nginx modificada para ejecutarse SIN privilegios de root
FROM nginxinc/nginx-unprivileged:alpine

# Copiar los archivos construidos. NOTA: Si usas Vite, la carpeta suele llamarse 'dist'. Si es React clásico, cámbialo a 'build'
COPY --from=build /app/dist /usr/share/nginx/html

# Los contenedores unprivileged de Nginx exponen por defecto el puerto 8080 en lugar del 80
EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]