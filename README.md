# oas2026_brenda_kubernetes-orquestation

# Laboratorio de Kubernetes

## 1. Exploración de Objetos de Kubernetes

### Pod
Es la **unidad más pequeña que se puede desplegar en Kubernetes**.  
Un Pod puede contener uno o más contenedores que comparten red y almacenamiento.

### Deployment
Es un objeto que permite **gestionar y actualizar Pods automáticamente**.  
Se encarga de la creación, actualización y administración de los Pods.

### ReplicaSet
Su función es **asegurar que siempre exista un número específico de Pods ejecutándose**.  
Si un Pod falla, ReplicaSet crea automáticamente otro para mantener la cantidad definida.

### Service
Permite **exponer los Pods para que puedan ser accedidos dentro o fuera del cluster**.  
Proporciona una **IP estable** y permite la comunicación entre aplicaciones.

---

# 2. Comandos ejecutados

## Crear namespace

```bash
kubectl create namespace laboratorio
```

## Crear ConfigMap

```bash
kubectl apply -f configmap.yaml
```

## Crear Secret

```bash
kubectl apply -f secret.yaml
```

## Crear Deployment

```bash
kubectl apply -f deployment.yaml
```

## Crear Service

```bash
kubectl apply -f service.yaml
```

## Ver pods

```bash
kubectl get pods -n laboratorio
```

## Ver Deployments

```bash
kubectl get deployments -n laboratorio
```

## Ver Services

```bash
kubectl get services -n laboratorio
```

## Ver detalles de un Pod

```bash
kubectl describe pod nombre-pod -n laboratorio
```

## Ver logs del contenedor

```bash
kubectl logs nombre-pod -n laboratorio
```

## Escalamiento de la aplicación

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.25 -n laboratorio
deployment.apps/nginx-deployment image updated
```
```bash
kubectl rollout status deployment nginx-deployment -n laboratorio
```

## Ver estado del despliegue

```bash
kubectl rollout status deployment nginx-deployment -n laboratorio
```

## Eliminar Deployment

```bash
kubectl delete deployment nginx-deployment -n laboratorio
```

## Eliminar Service

```bash
kubectl delete service nginx-service -n laboratorio
```

## Eliminar Namespace

```bash
kubectl delete namespace laboratorio
```

---

# 3. Buenas prácticas aplicadas

### Uso de Namespaces
Se utilizó un namespace específico para organizar los recursos del laboratorio y evitar conflictos con otros recursos del cluster.

### Uso de ConfigMap para configuración
La configuración de la aplicación se almacenó en un ConfigMap, permitiendo modificar valores sin cambiar la imagen del contenedor

### Uso de Secret
Las credenciales fueron almacenadas en un Secret, evitando exponer datos sensibles en archivos de configuración públicos.

### Uso de Deployment
Se utilizó Deployment para garantizar:
Recuperación automática de Pods
Escalabilidad
Actualizaciones controladas

### Uso de réplicas
Se configuraron 2 réplicas, lo que permite que la aplicación siga funcionando si un Pod falla.

### Uso de Labels
Se aplicaron labels para identificar los Pods y permitir que el Service pueda encontrarlos.
