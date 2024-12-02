
# JSON Server Project

Este proyecto utiliza `json-server` para servir datos en dos endpoints principales: `/estudiantes` y `/cursos`.

## Estructura del Proyecto

La estructura del proyecto es la siguiente:

```plaintext
/json-server-project
  ├── server/
  │   ├── db.json          # Archivo con los datos de los endpoints
  │   ├── routes.json      # (Opcional) Archivo para definir rutas personalizadas
  ├── package.json         # Configuración del proyecto y scripts de npm
  ├── node_modules/        # Dependencias del proyecto
```

## Requisitos Previos

Asegúrate de tener instalado:

- [Node.js](https://nodejs.org/) (incluye `npm`).

## Instalación

1. Clona este repositorio o descarga los archivos.
2. Navega al directorio del proyecto en tu terminal:

   ```bash
   cd json-server-project
   ```

3. Instala las dependencias:

   ```bash
   npm install
   ```

## Configuración de Endpoints

Los datos se encuentran definidos en el archivo `server/db.json`. Este archivo contiene dos colecciones:

- **Estudiantes**: Endpoint disponible en `/estudiantes`.
- **Cursos**: Endpoint disponible en `/cursos`.

Ejemplo de `db.json`:

```json
{
  "estudiantes": [
    {
      "studentId": 1,
      "name": "Alicia",
      "surname": "Pérez",
      "career": {
        "careerId": 1,
        "name": "Diseño"
      }
    }
  ],
  "cursos": [
    {
      "career": "Diseño",
      "course": "Diseño 101",
      "students": [
        {
          "studentId": 1,
          "name": "Alicia",
          "surname": "Pérez"
        }
      ]
    }
  ]
}
```

## Ejecutar el Servidor

1. Para iniciar el servidor JSON, utiliza el siguiente comando:

   ```bash
   npm run start:server
   ```

2. Esto iniciará el servidor en [http://localhost:3000](http://localhost:3000).

## Endpoints Disponibles

### 1. Estudiantes
Endpoint: [http://localhost:3000/estudiantes](http://localhost:3000/estudiantes)

Ejemplo de respuesta:

```json
[
  {
    "studentId": 1,
    "name": "Alicia",
    "surname": "Pérez",
    "career": {
      "careerId": 1,
      "name": "Diseño"
    }
  }
]
```

### 2. Cursos
Endpoint: [http://localhost:3000/cursos](http://localhost:3000/cursos)

Ejemplo de respuesta:

```json
[
  {
    "career": "Diseño",
    "course": "Diseño 101",
    "students": [
      {
        "studentId": 1,
        "name": "Alicia",
        "surname": "Pérez"
      }
    ]
  }
]
```

## Crear un nuevo estudiante (POST)

Puedes crear un nuevo estudiante utilizando el método `POST` en `/estudiantes`.

### Ejemplo:
```bash
curl -X POST http://localhost:3000/estudiantes -H "Content-Type: application/json" -d '{
  "studentId": 11,
  "name": "Laura",
  "surname": "Martínez",
  "career": {
    "careerId": 2,
    "name": "Informática"
  }
}'
```

## Eliminar un estudiante (DELETE)

Para eliminar un estudiante, usa el método `DELETE` en `/estudiantes/:id`.

### Ejemplo:
```bash
curl -X DELETE http://localhost:3000/estudiantes/11
```

## Personalización de Rutas (Opcional)

Si deseas personalizar las rutas, utiliza el archivo `server/routes.json`. Ejemplo:

```json
{
  "/students": "/estudiantes",
  "/courses": "/cursos"
}
```

Para usarlo, inicia el servidor con:

```bash
json-server --watch server/db.json --routes server/routes.json --port 3000
```

## Notas

- Asegúrate de que `json-server` esté instalado localmente con:

  ```bash
  npm install json-server --save-dev
  ```

- Puedes cambiar el puerto usando la opción `--port`. Ejemplo:

  ```bash
  npm run start:server -- --port 4000
  ```