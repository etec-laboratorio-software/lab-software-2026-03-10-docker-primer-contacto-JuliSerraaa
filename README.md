# MiEcommerce - Plataforma de E-commerce con Chat Integrado

Descripción del Proyecto

MiEcommerce es una plataforma completa de comercio electrónico desarrollada con React en el frontend y Node.js/Express en el backend, utilizando SQLite como base de datos. Incluye un sistema de mensajería en tiempo real entre compradores y vendedores.

---

## 🚀 Inicio Rápido con Docker (Recomendado)

### Requisitos previos:
- **Docker** instalado en tu sistema
- **Docker Compose** instalado

### Instalación en Linux:

```bash
# Instalar Docker (Ubuntu/Debian)
sudo apt-get update
sudo apt-get install docker.io docker-compose

# Dar permisos a tu usuario (para no usar sudo)
sudo usermod -aG docker $USER
newgrp docker

# Verificar que funciona
docker --version
docker-compose --version
```

### Ejecutar la aplicación:

Desde la **raíz del proyecto** (donde está `docker-compose.yml`):

```bash
# Construir e iniciar los contenedores
docker-compose up --build
```
En caso de que no funcione eso podras probar también:

```bash
docker compose up --build
```

✅ Verás algo como:
```
backend    | Modelos sincronizados con la base de datos (Tablas creadas/actualizadas).
backend    | Servidor Express corriendo en http://localhost:3000
frontend   | ➜  Local:   http://localhost
```

### Acceder a la aplicación:

Abre tu navegador en: **http://localhost**

---

## 🧪 Guía de Prueba Rápida

### Paso 1: Registrar dos usuarios

**Usuario 1 (Vendedor):**
- Username: `vendedor1`
- Email: `vendedor1@test.com`
- Password: `Password123`

**Usuario 2 (Comprador):**
- Username: `comprador1`
- Email: `comprador1@test.com`
- Password: `Password123`

### Paso 2: Crear productos (como vendedor1)

Inicia sesión como vendedor1 → Haz clic en "Vender" → Crea algunos productos:
- iPhone 13 Pro - $999.99
- Zapatillas Nike - $129.99

### Paso 3: Probar compras y chat (como comprador1)

Cierra sesión → Inicia sesión como comprador1 → Navega por productos → Haz clic en "💰 Comprar Ahora"

✅ Verás:
- Conversación automática creada
- Mensaje de compra automático
- Redirección al chat

### Paso 4: Verificar chat (como vendedor1)

Cierra sesión → Inicia sesión como vendedor1 → Haz clic en "Mensajes"

✅ Verás las conversaciones y podrás responder en tiempo real

---

## 🔧 Comandos útiles para Docker

```bash
# Ver logs en vivo
docker-compose logs -f

# Ver logs del backend
docker-compose logs -f backend

# Ver logs del frontend
docker-compose logs -f frontend

# Parar los contenedores
docker-compose down

# Parar y eliminar datos (⚠️ borra la base de datos)
docker-compose down -v

# Reconstruir después de cambios en código
docker-compose up --build

# Ejecutar en segundo plano
docker-compose up -d --build
```

---

## 🐛 Solucionar problemas

### El navegador no carga la app
```bash
# Espera 30 segundos después de ejecutar docker-compose up
# Los contenedores necesitan tiempo para compilar y iniciar

# Verifica los logs:
docker-compose logs
```

### Ver si los puertos están ocupados
```bash
# Linux
sudo lsof -i :80
sudo lsof -i :3000

# O alternativamente
ss -tulpn | grep -E ':80|:3000'
```

### Reconstruir completamente
```bash
docker-compose down
docker-compose up --build
```

### Limpiar caché de Docker
```bash
docker system prune -a
```

---

## 📦 Estructura Docker

```
docker-compose.yml        ← Orquestación
├── Backend/
│   ├── Dockerfile        ← Node.js 20 + SQLite
│   └── server.js
├── Frontend/
│   ├── Dockerfile        ← Vite + React + Nginx
│   ├── nginx.conf        ← Reverse proxy
│   └── src/
```

### Cómo funciona:
1. **Backend**: Express en puerto 3000 (interno)
2. **Nginx**: Sirve Frontend en puerto 80 + redirige `/api/` al backend
3. **Red Docker**: Los contenedores se comunican automáticamente por nombre (`backend`)
4. **Base de datos**: Persiste en `./Backend/data/`

---

## 💾 Datos persistentes

Tu base de datos SQLite se guarda en:
```
./Backend/data/database.sqlite
```

Esto significa que tus datos **persisten entre reinicios** de Docker. 🔒

---

## ✨ Características Principales

🏪 **Catálogo de productos** - Visualización y gestión  
🔐 **Sistema de autenticación** - Registro y login  
💬 **Chat en tiempo real** - Comunicación comprador-vendedor  
🛒 **Sistema de compras** - Proceso con un clic  

---

## 📝 Notas importantes

- La aplicación estará disponible en `http://localhost` (Puerto 80)
- El backend corre internamente en el puerto 3000 (no es accesible desde fuera)
- Los cambios en el código requieren: `docker-compose up --build`
- Los datos de la base de datos persisten en `./Backend/data/`

---

¡Tu plataforma de e-commerce con Docker está lista! 🚀
