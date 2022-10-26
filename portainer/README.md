# Portainer 2.7 en Kubernetes

## Instalación del repositorio Portainer en HELM

```bash
helm repo add portainer https://portainer.github.io/k8s/
helm repo update
```

## Verificación y contenido del repo

```bash
helm repo list
helm search repo -l
helm show readme <chart>
helm show values <chart>
```