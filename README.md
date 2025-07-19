# Informe de Implementación y Resultados del Proyecto DevOps

Repositorio: https://github.com/Luchito0703/proyectoDevOps

Luis Miguel López Uribe  
lulopezu@unal.edu.co  
David Moreno Gaviria  
davmorenoga@unal.edu.co  
Santiago Ortiz Cardona  
sanortizca@unal.edu.co  

Estudiantes de Administración de Sistemas Informáticos  
Universidad Nacional de Colombia  
Sede Manizales  

Introducción a DevOps  
Juan Camilo Escobar Naranjo  
2025  

## Contenido

1. Introducción  
2. Arquitectura y Tecnologías  
3. Control de Versiones con Git y Git Flow  
4. Contenerización con Docker  
5. Integración y Despliegue Continuo (CI/CD)  
6. Gestión de Artefactos con Nexus  
7. Monitoreo con Prometheus y Grafana  
8. Pruebas Unitarias  
9. Conclusiones y Lecciones Aprendidas  

---

## 1. Introducción

El presente informe detalla el proceso de implementación de un ciclo de vida DevOps completo para una aplicación de gestión de ventas desarrollada con el framework FastAPI. El objetivo principal del proyecto fue aplicar las metodologías y herramientas DevOps para automatizar la integración, el despliegue y la operación de la aplicación, garantizando la eficiencia, la fiabilidad y la escalabilidad del sistema.

Partiendo de una aplicación base, se implementó un flujo de trabajo que abarca desde el control de versiones con Git hasta el monitoreo en tiempo real con Prometheus y Grafana. El proyecto se estructuró para cumplir con los siguientes entregables clave: un repositorio versionado bajo la estrategia Git Flow, la contenerización de la aplicación y sus servicios dependientes, la configuración de un pipeline de Integración Continua y Despliegue Continuo (CI/CD) con GitHub Actions, la gestión de artefactos con un repositorio Nexus autoalojado y el despliegue final en un entorno basado en Docker Compose.

## 2. Arquitectura y Tecnologías

### 2.1. Arquitectura de la Solución

La arquitectura se centra en un modelo de servicios contenerizados, orquestados por Docker Compose. Los componentes principales son:

- **Servicio de Aplicación (fastapi-app)**: El núcleo de la solución. Es una API RESTful construida en FastAPI que expone endpoints para gestionar clientes, productos y ventas. Además, ofrece un endpoint `/metrics` para el monitoreo.  
- **Servicio de Monitoreo (prometheus)**: Recolecta periódicamente las métricas de FastAPI.  
- **Servicio de Visualización (grafana)**: Dashboards con métricas desde Prometheus.  
- **Servicio de Artefactos (nexus)**: Repositorio privado de imágenes Docker.  

Todos los servicios se comunican entre sí mediante la red `app-network` definida en `docker-compose.yml`.

### 2.2. Tecnologías Utilizadas

- Python y FastAPI  
- Git y Git Flow  
- Docker y Docker Compose  
- GitHub Actions  
- Nexus Repository Manager  
- Prometheus y Grafana  
- Pytest  

## 3. Control de Versiones con Git y Git Flow

Se adoptó Git Flow para separar ramas de desarrollo, producción y nuevas funcionalidades.

```bash
git flow feature start <nombre-feature>
# ...
git flow feature finish <nombre-feature>
```

Las ramas `feature` son eliminadas tras integrarse a `develop`.

## 4. Contenerización con Docker

### 4.1 Dockerfile

Pasos clave:

1. Imagen base Python  
2. Directorio de trabajo  
3. Instalar `requirements.txt`  
4. Copiar el código  
5. Exponer puerto 5000  
6. Iniciar con `uvicorn`

### 4.2 Docker Compose

Servicios definidos:

- app (Dockerfile local)  
- prometheus, grafana, nexus (imágenes oficiales)  
- Volúmenes persistentes  
- Red: app-network  

## 5. Integración y Despliegue Continuo (CI/CD)

Se diseñó un pipeline CI/CD con GitHub Actions para cada `push` a `develop` y `master`.

### CI

- Clonación  
- Configuración de Python  
- Instalación de dependencias  
- Pruebas con pytest  

### CD

- Construcción y push a Nexus  
- Despliegue remoto con docker-compose  

## 6. Gestión de Artefactos con Nexus

Nexus almacena imágenes Docker versionadas desde el pipeline. Esto desacopla la construcción del despliegue y permite hacer rollbacks.

## 7. Monitoreo con Prometheus y Grafana

### 7.1 Exposición de Métricas

Instrumentación con `prometheus_client`:

- `http_requests_total`  
- `http_request_duration_seconds`  

Middleware actualiza y expone métricas en `/metrics`.

### 7.2 Recolección y Visualización

Prometheus consulta `app:5000`. Grafana usa Prometheus como fuente de datos y muestra dashboards en tiempo real.

## 8. Pruebas Unitarias

Se utilizó `pytest` y `TestClient`.

### Casos de prueba (`tests/test_main.py`):

- `test_root`  
- `test_metrics`  
- `test_add_sale_success`  

### Resultado:

```
3 passed, 1 warning in 0.89s
```

**Advertencias**:

- `PytestDeprecationWarning`: sobre el scope de `asyncio`  
- `PydanticDeprecatedSince20`: `.dict()` obsoleto, usar `.model_dump()`

## 9. Conclusiones y Lecciones Aprendidas

- ✅ Automatización acelera entregas y evita errores  
- ✅ Contenerización garantiza entornos consistentes  
- ✅ Observabilidad es esencial desde el inicio  
- ✅ Buenas prácticas como Git Flow mejoran la calidad del proyecto  

---
