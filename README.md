# Proyecto SQL – Gestión de visitas a sucursales (Grupo Solvens)

Aplicación web para administrar el trabajo de **repositores** en sucursales de cadenas comerciales: carga de visitas con fotos, revisión y aprobación por parte de un administrador, y consulta de las imágenes aprobadas por parte del cliente.

## Roles

| Rol | Qué puede hacer |
|-----|-----------------|
| **Administrador** | Gestiona cadenas, sucursales, usuarios, categorías y productos. Revisa, aprueba o rechaza visitas e imágenes, y consulta reportes. |
| **Repositor** | Ve sus sucursales asignadas y carga visitas con fotos. |
| **Cliente** | Consulta las visitas e imágenes aprobadas de sus productos y sucursales. |

## Funcionalidades principales

- Login con contraseñas hasheadas (`bcrypt`).
- ABM de cadenas, sucursales, usuarios, categorías y productos.
- Carga de visitas con múltiples imágenes (`multer` + `sharp` para procesarlas).
- Flujo de aprobación/rechazo de visitas e imágenes.
- Filtros y reportes de visitas, y de carga de imágenes por cliente.

## Tecnologías

- **Backend:** Node.js, Express 5, PostgreSQL (`pg`)
- **Almacenamiento de imágenes:** Cloudflare R2 (API compatible con S3, `@aws-sdk/client-s3`)
- **Frontend:** HTML, CSS y JavaScript sin framework

## Estructura

```
.
├── CODIGO/
│   ├── *.html        # Pantallas (login, paneles, formularios, tablas)
│   ├── style/        # Hojas de estilo
│   └── js/
│       ├── server.mjs     # Servidor Express y API REST
│       ├── conexion.mjs   # Pool de conexión a PostgreSQL
│       ├── filtros.js     # Lógica de filtros del frontend
│       └── modal_confirmacion.js
├── IMG/              # Imágenes de ejemplo / visitas
├── package.json
└── README.md
```

## Puesta en marcha

1. Instalar dependencias:

   ```bash
   npm install
   ```

2. Definir las variables de entorno (por ejemplo en un archivo `.env`, que está ignorado por git):

   | Variable | Descripción |
   |----------|-------------|
   | `DATABASE_URL` | Cadena de conexión a PostgreSQL |
   | `R2_ACCOUNT_ID` | ID de cuenta de Cloudflare R2 |
   | `R2_ACCESS_KEY_ID` | Clave de acceso de R2 |
   | `R2_SECRET_ACCESS_KEY` | Clave secreta de R2 |
   | `R2_BUCKET_NAME` | Nombre del bucket |
   | `R2_PUBLIC_URL` | URL pública del bucket (ej: `https://pub-xxx.r2.dev`) |
   | `PORT` | Puerto del servidor (opcional, por defecto `3000`) |

3. Iniciar el servidor:

   ```bash
   node CODIGO/js/server.mjs
   ```

   El servidor queda disponible en `http://localhost:3000`.

> **Nota:** el script `npm start` apunta a `server.mjs` en la raíz, pero el archivo está en `CODIGO/js/`. Hasta que se ajuste el script, usá el comando de arriba.
