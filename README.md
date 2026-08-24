# Observatorio Tecnológico - Backend API

API REST para el Observatorio Tecnológico Regional, un sistema de análisis y seguimiento del ecosistema tecnológico centroamericano que permite monitorear empresas, productos, eventos sectoriales, indicadores económicos y tendencias tecnológicas.

## Descripción

El Observatorio Tecnológico es una plataforma integral que proporciona herramientas de análisis para:

- **Empresas tecnológicas**: Gestión y análisis de compañías del sector tech
- **Productos y servicios**: Catálogo de soluciones tecnológicas
- **Eventos sectoriales**: Seguimiento de inversiones, adquisiciones, hackeos y otros eventos relevantes
- **Indicadores económicos**: Métricas económicas por país
- **Tendencias tecnológicas**: Identificación y seguimiento de tecnologías emergentes
- **Análisis comparativo**: Comparativas entre países y sectores

## Tecnologías Utilizadas

- **Node.js** con **Express.js** - Framework web
- **PostgreSQL** - Base de datos relacional
- **Sequelize** - ORM para Node.js
- **JWT** - Autenticación y autorización
- **Passport.js** - Middleware de autenticación
- **Argon2** - Cifrado seguro de contraseñas
- **Swagger** - Documentación de API
- **Multer** - Manejo de archivos
- **Sharp** - Procesamiento de imágenes
- **Express Validator** - Validación de datos
- **Morgan** - Logger HTTP
- **Moment.js** - Manejo de fechas

## Arquitectura del Proyecto

```
src/
├── app.js                 # Punto de entrada de la aplicación
├── config/               # Configuraciones
│   ├── db.js            # Configuración de base de datos
│   ├── passport.js      # Configuración de autenticación
│   └── swagger.js       # Configuración de documentación
├── controllers/         # Lógica de negocio
│   ├── controladorAuth.js
│   ├── controladorEmpresa.js
│   ├── controladorEncuestaDemanda.js
│   ├── controladorEventoSector.js
│   ├── controladorFrontend.js    # Endpoints especiales para frontend
│   ├── controladorIndicadorEconomico.js
│   ├── controladorPais.js
│   ├── controladorProductoServicio.js
│   ├── controladorRegistrosAcceso.js
│   ├── controladorTendenciaTecnologica.js
│   └── controladorUsuario.js
├── models/              # Modelos de datos (Sequelize)
│   ├── empresa.js
│   ├── encuestaDemanda.js
│   ├── eventoSector.js
│   ├── indicadorEconomico.js
│   ├── pais.js
│   ├── productoServicio.js
│   ├── registroAcceso.js
│   ├── tendenciaTecnologica.js
│   └── usuario.js
├── routes/              # Definición de rutas
│   ├── index.js
│   ├── rutasAuth.js
│   ├── rutasEmpresa.js
│   ├── rutasEncuestaDemanda.js
│   ├── rutasEventoSector.js
│   ├── rutasFrontend.js      # Endpoints especializados
│   ├── rutasIndicadorEconomico.js
│   ├── rutasPais.js
│   ├── rutasProductoServicio.js
│   ├── rutasRegistroAcceso.js
│   ├── rutasTendenciaTecnologica.js
│   └── rutasUsuario.js
└── middlewares/         # Middlewares personalizados
```

## Modelo de Datos

### Entidades Principales

- **Países**: Información base de países centroamericanos
- **Empresas**: Compañías tecnológicas con datos como sector, empleados, año de fundación
- **Productos/Servicios**: Catálogo de soluciones tecnológicas por empresa
- **Eventos de Sector**: Inversiones, adquisiciones, hackeos, cierres de empresas
- **Indicadores Económicos**: Métricas económicas por país
- **Tendencias Tecnológicas**: Tecnologías emergentes
- **Usuarios**: Sistema de autenticación con roles (admin, analista, lector)
- **Registros de Acceso**: Auditoría de acciones de usuarios

### Relaciones

- Empresas ↔ Países (muchos a uno)
- Empresas ↔ Tendencias Tecnológicas (muchos a uno)
- Productos/Servicios ↔ Empresas (muchos a uno)
- Eventos ↔ Empresas (muchos a uno)
- Registros de Acceso ↔ Usuarios (muchos a uno)

## Instalación y Configuración

### Prerrequisitos

- Node.js (v14 o superior)
- PostgreSQL
- npm o yarn

### Pasos de Instalación

1. **Clonar el repositorio**
   ```bash
   git clone [URL_DEL_REPOSITORIO]
   cd ObservatorioBackend
   ```

2. **Instalar dependencias**
   ```bash
   npm install
   ```

3. **Configurar variables de entorno**
   
   Crear archivo `.env` en la raíz del proyecto:
   ```env
   # Base de datos
   DB_NAME=observatorio_db
   DB_USER=tu_usuario
   DB_PASSWORD=tu_contraseña
   DB_HOST=localhost
   DB_PORT=5432
   
   # Puerto del servidor
   PORT=3000
   
   # Clave JWT
   CLAVE=tu_clave_jwt_muy_segura
   ```

4. **Configurar base de datos PostgreSQL**
   ```sql
   CREATE DATABASE observatorio_db;
   ```

5. **Ejecutar la aplicación**
   ```bash
   # Desarrollo (con nodemon)
   npm run dev
   
   # Producción
   npm start
   ```

## 📡 Endpoints de API

### Autenticación
- `POST /api/auth/login` - Iniciar sesión

### Gestión de Países
- `GET /api/pais` - Listar países
- `GET /api/pais/buscar` - Buscar país por código
- `POST /api/pais` - Crear país
- `PUT /api/pais` - Actualizar país
- `DELETE /api/pais` - Eliminar país

### Gestión de Empresas
- `GET /api/empresa` - Listar empresas
- `GET /api/empresa/buscar` - Buscar empresa por ID
- `POST /api/empresa` - Crear empresa
- `PUT /api/empresa` - Actualizar empresa
- `DELETE /api/empresa` - Eliminar empresa

### Productos y Servicios
- `GET /api/producto-servicio` - Listar productos/servicios
- `GET /api/producto-servicio/buscar` - Buscar por ID
- `POST /api/producto-servicio` - Crear producto/servicio
- `PUT /api/producto-servicio` - Actualizar producto/servicio
- `DELETE /api/producto-servicio` - Eliminar producto/servicio

### Eventos de Sector
- `GET /api/evento-sector` - Listar eventos
- `GET /api/evento-sector/buscar` - Buscar evento por ID
- `POST /api/evento-sector` - Crear evento
- `PUT /api/evento-sector` - Actualizar evento
- `DELETE /api/evento-sector` - Eliminar evento

### Endpoints Especiales para Frontend
- `GET /api/frontend/comparativa-paises` - Comparativa entre países
- `GET /api/frontend/eventos-por-fecha` - Eventos en rango de fechas
- `GET /api/frontend/empresas-internacionales` - Empresas con presencia internacional
- `GET /api/frontend/productos-por-sector` - Productos agrupados por sector
- `GET /api/frontend/ranking-paises-empresas` - Ranking de países por número de empresas
- `GET /api/frontend/empresas-mayor-crecimiento` - Empresas de mayor crecimiento
- `GET /api/frontend/distribucion-empresas` - Distribución geográfica de empresas
- `GET /api/frontend/comparar-indicadores` - Comparar indicadores entre países
- `GET /api/frontend/indicadores-por-pais` - Indicadores de un país específico
- `GET /api/frontend/eventos-por-tipo` - Filtrar eventos por tipo
- `GET /api/frontend/empresas-por-tendencia` - Empresas por tendencia tecnológica
- `GET /api/frontend/tendencias-emergentes` - Tendencias tecnológicas emergentes
- `GET /api/frontend/productos-mas-demandados` - Top 10 productos más demandados
- `GET /api/frontend/detalle-empresa` - Detalle completo de empresa
- `GET /api/frontend/empresas-por-pais-sector` - Filtrar empresas por país/sector
- `GET /api/frontend/buscar-empresa` - Búsqueda por nombre o palabra clave
- `GET /api/frontend/empresas-influyentes` - Top 10 empresas más influyentes

## Documentación API

La documentación completa de la API está disponible através de Swagger:

```
http://localhost:3000/api-docs
```

La documentación incluye:
- Descripción detallada de todos los endpoints
- Esquemas de datos
- Ejemplos de peticiones y respuestas
- Información de autenticación requerida

## Autenticación y Autorización

El sistema utiliza JWT (JSON Web Tokens) para la autenticación. Los usuarios tienen diferentes roles:

- **Admin**: Acceso completo al sistema
- **Analista**: Acceso de lectura/escritura limitado
- **Lector**: Solo acceso de lectura

### Uso de la Autenticación

1. Hacer login en `/api/auth/login`
2. Incluir el token JWT en el header de las peticiones:
   ```
   Authorization: Bearer [tu_token_jwt]
   ```

## Características Especiales

### Análisis Avanzado
- Comparativas entre países
- Rankings de empresas por diversos criterios
- Análisis de tendencias tecnológicas
- Métricas de crecimiento empresarial

### Filtros y Búsquedas
- Búsqueda por múltiples criterios
- Filtros por país, sector, tipo de evento
- Rangos de fechas
- Búsqueda de texto libre

### Auditoría
- Registro de todas las acciones de usuarios
- Tracking de accesos al sistema
- Histórico de cambios

## Configuración de Desarrollo

### Scripts Disponibles

```bash
# Desarrollo con recarga automática
npm run dev

# Ejecución normal
npm start

# Tests (por implementar)
npm test
```

### Variables de Entorno

| Variable | Descripción | Valor por Defecto |
|----------|-------------|-------------------|
| `PORT` | Puerto del servidor | 3000 |
| `DB_NAME` | Nombre de la base de datos | - |
| `DB_USER` | Usuario de PostgreSQL | - |
| `DB_PASSWORD` | Contraseña de PostgreSQL | - |
| `DB_HOST` | Host de la base de datos | localhost |
| `DB_PORT` | Puerto de PostgreSQL | 5432 |
| `JWT_SECRET` | Clave secreta para JWT | - |

## Despliegue

### Preparación para Producción

1. Configurar variables de entorno de producción
2. Configurar base de datos PostgreSQL en producción
3. Configurar HTTPS y certificados SSL
4. Configurar proxy reverso (nginx recomendado)
5. Configurar monitoreo y logs

### Consideraciones de Seguridad

- Usar HTTPS en producción
- Configurar CORS apropiadamente
- Validar todas las entradas de datos
- Implementar rate limiting
- Mantener dependencias actualizadas

**Observatorio Tecnológico Regional** - Monitoreo y análisis del ecosistema tecnológico centroamericano.