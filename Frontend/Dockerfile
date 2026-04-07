# Etapa 1: Compilar la aplicación React usando Vite
FROM node:20-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

# Etapa 2: Servir la aplicación estática usando Nginx
FROM nginx:alpine

# Remueve los archivos por defecto de Nginx
RUN rm -rf /usr/share/nginx/html/*

# Copia los archivos estáticos desde la etapa previa (carpeta /dist en Vite)
COPY --from=build /app/dist /usr/share/nginx/html

# Copia nuestra configuración personalizada de Nginx para el puerto 80
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
