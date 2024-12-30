# Gestión de tareas

Este proyecto es un sistema backend sólido para gestionar usuarios, tareas. Está desarrollado con Node.js, Express y MongoDB, y utiliza TypeScript para la seguridad de tipos y una mejor experiencia para los desarrolladores.

## Características

- Autenticación y autorización de usuarios
- Control de acceso basado en roles (RBAC)
- Gestión de usuarios (operaciones CRUD)
- Gestión de tareas (operaciones CRUD)
- Middleware personalizado para autenticación y permisos basados ​​en roles
- Integración con MongoDB para persistencia de datos
- TypeScript para una mejor verificación de tipos y calidad del código

## Tecnologías utilizadas

- Node.js
- Express.js
- TypeScript
- MongoDB
- Mongoose (ODM)
- JSON Web Tokens (JWT) para autenticación

## Estructura del proyecto

El proyecto esta estructurado de la siguiente manera:

- `src/`: Contiene el codigo TypeScript necesario
  - `controllers/`: Maneja el procesamiento de solicitudes y la generación de respuestas.
  - `middlewares/`: Middleware personalizado para autenticación y permisos
  - `models/`: Modelos Mongoose para la interacción con bases de datos
  - `repositories/`: Capa de acceso a datos para operaciones de base de datos
  - `routes/`: Definiciones de rutas API
  - `services/`: Capa de lógica empresarial
  - `types/`: Definiciones de tipos de TypeScript
- `dist/`: Código compilado JavaScript
- `@types/`: Definiciones de tipos personalizados para bibliotecas externas

## Primeros pasos

### Requisitos previos

- Node.js (v22)
- MongoDB

### Instalación

1. Clona el repositorio:

```
git clone https://github.com/your-username/your-repo-name.git
```

2. Instala las dependencias:

```
npm install
```

3. Configura las variables de entorno (crea un archivo `.env` en el directorio raíz):

```
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
PORT=8000
```

4. Crea el código TypeScript:

```
npm run build
```

5. Inicia el servidor:
```
npm start
```

## Crear roles y permiso.

Para poder crear los datos iniciales se debe de Comentar la linea siguiente en el directorio `routes/`

``` router.post("/roles", verifyToken, getPermissons, createRoles);
```
luego Descomentar

``` router.post("/roles", createRoles);
```
Este paso es para poder dar acceso a las rutas sin restrinsión de acceso luego de debe de dejar todo como estaba inicialmente.

### Debe de enviar la siguiente estructura de datos

1. Creación del Rol User y sus permisos
```
{
  "name": "user",
  "permissions": [
      "task_write",
      "task_read",
      "tasl_update",
      "task_delete"
  ]
}
```

2. Creación del Rol Admin y sus permisos
```
{
  "name": "admin",
  "permissions": [
      "admin_granted"
  ]
}
```
## Creación de usuarios

Para poder crear los datos iniciales se debe de Comentar la linea siguiente

```router.post("/users", verifyToken, getPermissons, checkRoles, createUser);
```
luego Descomentar

```router.post("/users", createUser);
```
Este paso es para poder dar acceso a las rutas sin restrinsión de acceso luego de debe de dejar todo como estaba inicialmente.


### Se debe de enviar la siguiente estructura de datos

1. Creación de usuario con rol user

```
{
  "name": "name_user",
  "username": "username",
  "email": "email_user",
  "password":"password_user",
  "roles":[user]
}
```

2. Creación de usuario con rol admin

```
{
  "name": "name_user",
  "username": "username",
  "email": "email_user",
  "password":"password_user",
  "roles":[admin]
}
```
En tal caso tambien puede realizarlo directamente en la Base de datos manualmente

## Uso

La API proporciona endpoint para la administración de usuarios, la autenticación, la administración de roles y las operaciones de publicación de tareas. 

### Endpoints

- Autenticación: `/api/auth/login`, `/api/auth/register`
- Usuarios: `/api/users`
- Roles: `/api/roles`
- Tareas: `/api/task`

Consulte los archivos de ruta para obtener una lista completa de los puntos finales disponibles y sus funcionalidades.

## Desarrollo

Para el desarrollo, puede utilizar los siguientes scripts npm:

- `npm run dev`: Inicia el servidor de desarrollo con recarga en caliente
- `npm run build`: Compila TypeScript a JavaScript
- `npm start`: Inicia el servidor de producción
