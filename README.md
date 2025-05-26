# LMS-clinical-simulation

[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/TG-16-PUJ-2025-01/LMS-clinical-simulation)

## Introducción
- Nombre del proyecto: Sistema de gestión de aprendizaje para el Centro de Simulación Clínica de la Pontificia Universidad Javeriana 
- Descripción: Aplicación web para visualizar, calificar y retroalimentar videos de simulaciones académicas. El objetivo es simplificar el trabajo de los profesores al momento de calificar, permitiendo que los estudiantes no solo puedan entender dónde se equivocaron, sino también poder reclamar con evidencias en el caso de que no esté de acuerdo.  
- Propósito del documento: Guiar a futuros desarrolladores y administradores en la comprensión, despliegue, mantenimiento y extensión del sistema. 

## Descripción general del sistema
- Arquitectura: Monolito distribuido (BackEnd/FrontEnd)

- Tecnologías utilizadas:
  - Backend: Spring Boot 3.4.2 (Java)
  - Frontend: React 18 (TypeScript)
  - Base de datos: PostgreSQL 14
  - Contenedores: Docker
  - Orquestación: Docker Compose
  - Testing: Cypress, Junit 5 + Mockito, Testcontainers

- Módulos de la aplicación:
  - Autenticación
  - Gestión administrativa (asignaturas, clases, miembros de clase, usuarios, salas y videos)
  - Reserva de prácticas
  - Visualización de videos
  - Gestión de rúbricas plantilla
  - Calificación de estudiantes
  - Visualización de calendario

## Estructura del repositorio
El proyecto está organizado en dos submódulos principales: `front-LMS-clinical-simulation` y `back-LMS-clinical-simulation`. La estructura del repositorio es la siguiente:
```
.
├── front-LMS-clinical-simulation/
├── back-LMS-clinical-simulation/
├── .env.template
├── LICENSE
├── docker-compose.prod-cloud.yml
├── docker-compose.prod.yml
└── docker-compose.yml
```

Para ver la estructura de cada submódulo, consulta sus respectivos archivos `README.md`.

## Instalación y configuración

### Desarrollo y Pruebas

- Requisitos previos:
  - Java 17 o superior.
  - Node.js 22 o superior.
  - Docker y Docker Compose.

1. Clonar el repositorio:
```bash
git clone https://github.com/TG-16-PUJ/LMS-clinical-simulation.git
cd LMS-clinical-simulation
```

2. Configurar las variables de entorno:
<br/>
Copia el archivo `.env.template` a `.env` y ajusta las variables de entorno.

3. Configurar el multi repo:

```bash
# Trae los submódulos y actualiza sus referencias
git submodule update --init
# Cambia la rama de los submódulos a main
git submodule foreach git checkout main
# Baja los últimos cambios de los submódulos
git submodule foreach git pull
```
4. Construir y ejecutar el entorno de desarrollo:

- Inicia la base de datos PostgreSQL:
```bash
docker compose up -d
```

- Inicia el backend:
```bash
cd back-LMS-clinical-simulation
./mvnw spring-boot:run
```

- Inicia el frontend:
```bash
cd front-LMS-clinical-simulation
npm install
node --run dev # Solo disponible en node 22 o superior
# (lo mismo que `npm run dev`)
```

- Ejecutar pruebas unitaria y de integración:
```bash
cd back-LMS-clinical-simulation
./mvnw test
```

- Ejecutar pruebas de extremo a extremo (E2E):
```bash
cd front-LMS-clinical-simulation
# Entorno de cypress
node --run cypress # Solo disponible en node 22 o superior
# (lo mismo que `npm run cypress`)
# En terminal
npx cypress run
```

- Ejecutar todo el proyecto con Docker Compose:
```bash
docker compose -f docker-compose.prod.yml up -d
```

### Producción
- Requisitos previos:
  - Docker y Docker Compose.

1. Clonar el repositorio:
```bash
git clone https://github.com/TG-16-PUJ/LMS-clinical-simulation.git
cd LMS-clinical-simulation
```

2. Configurar las variables de entorno:
<br/>
Copia el archivo `.env.template` a `.env` y ajusta las variables de entorno.

3. Ejecutar el entorno de producción:
```bash
docker compose -f docker-compose.prod-cloud.yml up -d
```

### Despliegue de nuevas versiones

Para desplegar nuevas versiones del sistema, sigue estos pasos:
1. Asegúrate de que todos los cambios estén comprometidos y empujados al repositorio en la rama `main` del repositorio principal y de cada submódulo.

2. Construye las imágenes de Docker:
- backend:
```bash
# Cambia la <versión> por la versión que desees
docker image build -t ghcr.io/tg-16-puj-2025-01/back-lms-clinical-simulation:<versión> ./back-LMS-clinical-simulation
# Construye otra imagen con el tag latest
docker image build -t ghcr.io/tg-16-puj-2025-01/back-lms-clinical-simulation:latest ./back-LMS-clinical-simulation
```

- frontend:
```bash
# Cambia la <versión> por la versión que desees
docker image build -t ghcr.io/tg-16-puj-2025-01/front-lms-clinical-simulation:<versión> ./front-LMS-clinical-simulation
# Construye otra imagen con el tag latest
docker image build -t ghcr.io/tg-16-puj-2025-01/front-lms-clinical-simulation:latest ./front-LMS-clinical-simulation
```

3. Sube las imágenes al registro de GitHub:
```bash
docker push ghcr.io/tg-16-puj-2025-01/back-lms-clinical-simulation:<versión>
docker push ghcr.io/tg-16-puj-2025-01/back-lms-clinical-simulation:latest
docker push ghcr.io/tg-16-puj-2025-01/front-lms-clinical-simulation:<versión>
docker push ghcr.io/tg-16-puj-2025-01/front-lms-clinical-simulation:latest
```

Ya queda configurado, si deseas ejecutar el entorno de [producción](#producción) con versiones específicas, puedes cambiar el archivo `docker-compose.prod-cloud.yml` para que use las imágenes con la versión específica.

## Recursos adicionales
Documentación autogenerada del repositorio:

[![Ask DeepWiki](https://deepwiki.com/badge.svg)](https://deepwiki.com/TG-16-PUJ-2025-01/LMS-clinical-simulation)

Documentación en swagger del backend:

- Ejecuta el backend y accede a la documentación en: 
http://localhost:8080/swagger-ui/index.html
- También puedes acceder a la documentación de la API en formato OpenAPI en:
http://localhost:8080/v3/api-docs
