# Traefik 2.5 en Kubernetes

## Instalación del repositorio Traefik en HELM

```bash
helm repo add traefik https://helm.traefik.io/traefik
helm repo update
```
[Traefik Documentation: Installation](https://doc.traefik.io/traefik/getting-started/install-traefik/#use-the-helm-chart)

## Verificación y contenido del repo

```bash
helm repo list
helm search repo -l
helm show readme <chart>
helm show values <chart>
```

## Crear archivo propio de valores para la instalación

* Primero generamos un archivo con los valores base del chart
```bash
helm show values traefik/traefik > my-values.yaml
```
Borramos todo lo que no queremos modificar, y dejamos los parámetros que nos interesa configurar en nuestro deploy

* Instalamos Traefik con los parámetros personales que definimos
```bash
kubectl create namespace ingress
helm install --values=./my-values.yaml --namespace=ingress traefik traefik/traefik
```

* Verificamos si el deploy fue exitoso
```bash
helm list --all-namespaces
helm status -n ingress traefik
```

* Acceso al dashboard de Traefik, y las métricas de traefik
Redireccionamos el puerto para poder acceder desde un browser local
```bash
kubectl port-forward <pod de traefik> 9000
```
Ese comando redirecciona el puerto 9000 local al puerto 9000 del pod, donde escucha el dasboard. Se accede con la URL:
http://localhost:9000/dashboard/
<br>

```bash
kubectl port-forward <pod de traefik> 9100
```
Ese comando redirecciona el puerto 9100 local al puerto 9100 del pod, donde escuchan las métricas de Traefik. Se accede con la URL:
http://localhost:9100/metrics/
