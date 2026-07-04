# Tienda de Perritos — Despliegue en AWS EKS

Proyecto de la asignatura Introducción a Herramientas DevOps (EA3), que implementa el despliegue de una aplicación de gestión de productos ("Tienda de Perritos") sobre una arquitectura de microservicios orquestada con Kubernetes, utilizando Amazon EKS como servicio administrado.

## Arquitectura

La aplicación está compuesta por tres microservicios independientes, cada uno en su propio contenedor Docker:

- **Frontend**: interfaz web servida con Nginx, permite listar, crear, editar y eliminar productos.
- **Backend**: API REST construida en Node.js/Express, expone los endpoints de productos y gestiona la conexión con la base de datos.
- **Base de datos**: MySQL, almacena el catálogo de productos.

Los tres servicios se comunican dentro del clúster mediante DNS interno de Kubernetes, y el frontend queda expuesto públicamente a través de un Service de tipo LoadBalancer.

## Infraestructura

- **Clúster:** Amazon EKS (`tienda-eks`), Kubernetes 1.34
- **Red:** VPC dedicada con subredes públicas y privadas distribuidas en 2 zonas de disponibilidad
- **Registro de imágenes:** Amazon ECR (repositorios independientes por servicio)
- **Autoescalado:** Horizontal Pod Autoscaler (HPA) basado en consumo de CPU
- **CI/CD:** GitHub Actions, con build automático de imágenes, push a ECR y despliegue en el clúster ante cada cambio en la rama `main`

## Estructura del repositorio
.
├── backend/          # API REST (Node.js + Express)
├── frontend/          # Interfaz web (HTML/JS + Nginx)
├── db/               # Base de datos MySQL (imagen + script de inicialización)
├── k8s/              # Manifiestos de Kubernetes (Deployments, Services, HPA, Secrets)
└── .github/workflows/ # Pipeline de integración y despliegue continuo

## Tecnologías utilizadas

Docker · Kubernetes · Amazon EKS · Amazon ECR · GitHub Actions · Node.js · MySQL · Nginx

## Autor

Aracely Escobar 
Asignatura: Introducción a Herramientas DevOps
