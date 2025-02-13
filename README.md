# 📌 VoxCorp - Guía de Instalación y Ejecución

Este proyecto incluye:
- **Frontend**: Angular
- **Backend**: Symfony
- **Base de Datos**: MySQL

---

## 🛠️ Requisitos Previos
Asegúrate de tener instalados los siguientes programas en tu sistema:

- **Git** ([Descargar](https://git-scm.com/))
- **Node.js** y **npm** ([Descargar](https://nodejs.org/))
- **Angular CLI** ([Instalar](https://angular.io/cli))
- **PHP** ([Descargar](https://www.php.net/downloads.php))
- **Composer** ([Descargar](https://getcomposer.org/))
- **MySQL** ([Descargar](https://dev.mysql.com/downloads/))

Opcional:
- **Symfony CLI** ([Instalar](https://symfony.com/download))
- **Docker** y **Docker Compose** (para ambiente con contenedores)

---

## 📥 1. Clonar el Repositorio

Ejecuta el siguiente comando en tu terminal:
```sh
 git clone https://github.com/amdress/VoxCorp.git
 cd VoxCorp
```

---

## 🚀 2. Configurar el Backend (Symfony)

### 🔹 2.1. Ir al directorio del backend
```sh
cd voxCorpApi
```

### 🔹 2.2. Instalar dependencias
```sh
composer install
```

### 🔹 2.3. Configurar el archivo `.env`
```sh
cp .env.example .env
```
Edita `.env` y configura la conexión con MySQL:
```
DATABASE_URL="mysql://usuario:contraseña@127.0.0.1:3306/voxcorp_db"
```

### 🔹 2.4. Crear la base de datos y ejecutar migraciones
```sh
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
```

### 🔹 2.5. Ejecutar el servidor de Symfony
```sh
symfony server:start
```
Si no tienes Symfony CLI, usa:
```sh
php -S localhost:8000 -t public
```

---

## 🎨 3. Configurar el Frontend (Angular)

### 🔹 3.1. Ir al directorio del frontend
```sh
cd ../voxCorp-frontend
```

### 🔹 3.2. Instalar dependencias
```sh
npm install
```

### 🔹 3.3. Configurar variables de entorno
Edita `src/environments/environment.ts` y coloca la URL del backend:
```ts
export const environment = {
  production: false,
  apiUrl: 'http://localhost:8000/api'
};
```

### 🔹 3.4. Ejecutar el servidor de Angular
```sh
ng serve
```
Abre el navegador en: **http://localhost:4200**

---

## 🔗 4. Acceder a la Aplicación
✔ **Frontend (Angular)**: [http://localhost:4200](http://localhost:4200)  
✔ **Backend (Symfony - API)**: [http://localhost:8000/api](http://localhost:8000/api)  

---

## 🐳 5. Opcional: Configurar Docker para MySQL
Si no quieres instalar MySQL manualmente, usa Docker:

### 📄 Crear archivo `docker-compose.yml` en la raíz del proyecto
```yaml
version: '3.8'
services:
  mysql:
    image: mysql:latest
    container_name: voxcorp-mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: voxcorp_db
      MYSQL_USER: usuario
      MYSQL_PASSWORD: contraseña
    ports:
      - "3306:3306"
    volumes:
      - mysql_data:/var/lib/mysql
volumes:
  mysql_data:
```

### 🚀 Iniciar MySQL con Docker
```sh
docker-compose up -d
```

---

## 📝 Notas Adicionales
- Si tienes problemas con permisos en Symfony, ejecuta:
  ```sh
  chmod -R 777 var/
  ```
- Si Angular no carga cambios, prueba:
  ```sh
  ng serve --open --poll=2000
  ```
- Para detener MySQL en Docker:
  ```sh
  docker-compose down
  ```

---

## 📌 Autor
**Miguel Andres de Cavalcante**  
📧 Contacto: [Tu Email o LinkedIn]

