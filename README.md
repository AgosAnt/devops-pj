# Proyecto Final — Infraestructura DevOps en la Nube

Proyecto universitario para el curso de infraestructura y DevOps. Consiste en desplegar una API REST en AWS usando contenedores, automatización y monitoreo en tiempo real.

## ¿Qué hace esto?

Cada vez que se hace un push a este repositorio, GitHub Actions compila el código, construye una imagen Docker, la sube a Amazon ECR y la despliega automáticamente en un servidor EC2. Sin intervención manual.

La aplicación es una API REST en Java con Spring Boot, conectada a PostgreSQL, con Prometheus recolectando métricas y Grafana mostrándolas en dashboards.

## Stack

- **Lenguaje:** Java 17 + Spring Boot
- **Contenedores:** Docker + Docker Compose
- **CI/CD:** GitHub Actions
- **Cloud:** AWS (EC2, ECR, VPC)
- **Base de datos:** PostgreSQL 15
- **Monitoreo:** Prometheus + Grafana

## Endpoints

| Método | Ruta | Descripción |
|--------|------|-------------|
| GET | `/api/items` | Lista todos los items |
| POST | `/api/items` | Crea un item nuevo |
| GET | `/api/items/health` | Estado del servidor |

## Estructura del proyecto
devops-pj/
├── api/
│   ├── src/                  # Código fuente Java
│   ├── Dockerfile            # Imagen de la aplicación
│   ├── docker-compose.yml    # App + DB + Prometheus + Grafana
│   └── prometheus.yml        # Configuración de métricas
├── k8s/
│   ├── deployment.yaml       # Configuración Kubernetes
│   └── service.yaml          # Exposición del servicio
└── .github/
└── workflows/
└── deploy.yml        # Pipeline CI/CD

## Infraestructura en AWS

- VPC con subredes públicas y privadas
- Instancia EC2 t3.micro con Ubuntu 24.04
- Amazon ECR como registro de imágenes Docker
- Security Groups configurados para HTTP, HTTPS y SSH

## Cómo funciona el pipeline

1. Se hace push a la rama `main`
2. GitHub Actions compila el proyecto con Maven
3. Construye la imagen Docker y la sube a ECR
4. Se conecta por SSH al servidor EC2
5. Descarga los cambios y reconstruye los contenedores

## Monitoreo

Prometheus recolecta métricas de la API cada 15 segundos a través del endpoint `/actuator/prometheus`. Grafana las visualiza en dashboards con CPU, memoria y requests por segundo.

---

Jonatan Santiago · Universidad Mariano Gálvez · 2026
