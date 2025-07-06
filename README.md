# proyectoDevOps
#Luis Miguel López Uribe - David Moreno Gaviria - Santiago Ortiz Cardona

En este taller, los estudiantes deberán implementar una solución DevOps integral que abarque todas las fases del ciclo de vida de una aplicación, desde el versionamiento del código hasta el monitoreo en producción. A partir de un proyecto base desarrollado en FastAPI para la gestión de clientes, productos y ventas, el reto consiste en contenerizar la aplicación, configurar un pipeline CI/CD completo mediante GitHub Actions, almacenar los artefactos en un repositorio Nexusautoalojado y exponer métricas que serán recolectadas por Prometheus y visualizadas en Grafana.

Además, el estudiante deberá realizar el despliegue automatizado de la aplicación en un entorno de producción, el cual podrá ser una instancia EC2 en AWS o un entorno de contenedores locales con Docker Compose. Se espera el uso de buenas prácticas de versionamiento con Git (incluyendo estrategias de branching), implementación de pruebas automáticas, construcción de imágenes, despliegue automático y exposición de métricas por medio del path /metrics.

Características:

Versionamiento colaborativo con Git

CI/CD con GitHub Actions

Contenerización con Docker

Publicación de artefactos en Nexus

Monitoreo de métricas con Prometheus y visualización con Grafana
Despliegue en una instancia EC2 o contendores locales
Entregables:

Repositorio Git versionado con la estrategia Git Flow
Dockerfile funcional para la aplicación
Archivo docker-compose.yaml que incluya Servicio de FastApi, Prometheus, Grafana  y nexus.
Pipelines de CI/CD con Github Actions
Informe de implementación y resultados
