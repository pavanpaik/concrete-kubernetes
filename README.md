# Concrete5.7 CDN on Kubernetes

This project can be used to provision Concrete 5.7 CDN on any kubernetes cluster.

Implemented by following the stateful app setup example provided in kubernetes documentation. 
https://kubernetes.io/docs/tutorials/stateful-application/mysql-wordpress-persistent-volume/


## Setup

### Verifgy that kubectl is installed

```kubectl version```

### Create a Secret for MySQL Password

```
kubectl create secret generic mysql-pass --from-literal=password=YOUR_PASSWORD
kubectl create secret generic mysql-root-pass --from-literal=password=YOUR_PASSWORD
```

### Deploy MySQL

```kubectl create -f mysql-deployment.yaml```

### Deploy WordPress

```kubectl create -f concrete-deployment.yaml```

### Verify status of all nodes using

```kubectl get all```

### Test

Access the following URL in browser - http://localhost/

Enter details for first access.
```
Server: concrete-mysql
MySQL User Name: c5db_user
MySQL Password: YOUR_PASSWORD
Database Name: c5db
```

## Cleaning up

### Delete your Secret

```
kubectl delete secret mysql-pass
kubectl delete secret mysql-root-pass
```

### Delete all Deployments and Services

```
kubectl delete deployment -l app=concrete-kubernetes
kubectl delete service -l app=concrete-kubernetes
kubectl delete pvc -l app=concrete-kubernetes
```

### Delete the PersistentVolumeClaims

```kubectl delete pvc -l app=concrete-kubernetes```