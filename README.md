# apuestas-service

Microservicio de **apuestas deportivas** del casino (FastAPI). Comparte la base de
datos PostgreSQL y el `JWT_SECRET` con `casino-backend` (no tiene login propio:
valida el JWT que emite el backend). Lista eventos con cuotas 1X2, registra
apuestas, **simula** el partido (modelo Poisson) y liquida las apuestas; los
equipos/escudos se siembran desde thesportsdb.

- Prefijo de rutas: `/api/apuestas` · Docs: `/docs`

## Endpoints
| Método | Ruta | Descripción |
|---|---|---|
| GET | `/api/apuestas/eventos` | Eventos abiertos con cuotas y escudos |
| POST | `/api/apuestas` | Registrar una apuesta (debita saldo) |
| GET | `/api/apuestas/mis-apuestas` | Apuestas del usuario |
| POST | `/api/apuestas/eventos/{id}/simular` | Simula y liquida el partido |
| POST | `/api/apuestas/reiniciar` | Regenera la cartelera |

## Ejecutar en local
```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
# variables: copia .env.example a .env y ajústalas
uvicorn app.main:app --reload --port 8005
```
Requiere una PostgreSQL accesible con las tablas compartidas (`usuarios`,
`transacciones`) que crea `casino-backend`.

## Despliegue en AWS EKS (Kubernetes) - EA3
Este servicio ha sido desplegado exitosamente en AWS EKS como parte de la Experiencia de Aprendizaje 3.

- **Rutas de salud**: Implementadas (`/health/liveness` y `/health/readiness`).
- **Docker**: Contenerizado mediante `Dockerfile` y alojado en **Amazon ECR**.
- **CI/CD**: Workflow de GitHub Actions configurado para construir y desplegar automáticamente en EKS.
- **Kubernetes**: Manifiestos de `Deployment`, `Service` y `HorizontalPodAutoscaler` aplicados.
- **Pruebas de Carga**: Validado mediante Locust con escalado automático (HPA) funcionando correctamente.
