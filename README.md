# Microservicio de Apuestas

Microservicio en Python (FastAPI/Flask) para la gestión del casino.

## Construir (Build)
Para instalar las dependencias localmente usando pip:
```bash
pip install -r requirements.txt
```

## Probar (Test)
Para ejecutar las pruebas unitarias:
```bash
pytest tests/
```

## Desplegar (Deploy)
El despliegue es automático a través de GitHub Actions en la rama `deploy`. Al hacer push, el pipeline probará el código, generará la imagen Docker, la enviará a Amazon ECR y actualizará los pods en Amazon EKS.

## Troubleshooting
- **ErrImagePull**: Verifica que el repositorio ECR exista en AWS y tenga permisos.
- **Microservicio caído**: Revisa los logs de Kubernetes usando `kubectl logs deployment/apuestas-service`.
