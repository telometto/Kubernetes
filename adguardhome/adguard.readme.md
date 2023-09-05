# Deployment
---
## How to deploy
🛑 **!! WARNING !!** 🛑

Unless you for some reason have to bootstrap the initial conf, I highly recommend you remove `kubectl apply -f adguard-configmap.yml`; ConfigMaps are immutable, so ***if you apply a configmap and destroy/re-deploy/reboot your machine, you will have to go through the configuration of your AGH container all over again!*** You have been warned!
```sh
sudo kubectl apply -f adguard-namespace.yml && \
sudo kubectl apply -f adguard-pv.yml && \
sudo kubectl apply -f adguard-pvc.yml && \
sudo kubectl apply -f adguard-configmap.yml && \ # you'll likely want to remove this line
sudo kubectl apply -f adguard-deployment.yml && \
sudo kubectl apply -f adguard-service.yml
```

## How to destroy
Again, if you didn't apply the `adguard-configmap.yml`, remove it from the commands below, too.
```sh
sudo kubectl delete service adguard-service -n adguard && \
sudo kubectl delete deployment adguard-deployment -n adguard && \
sudo kubectl delete configmap adguard-config -n adguard && \ # you'll likely want to remove this line
sudo kubectl delete pvc adguard-pvc-conf -n adguard && \
sudo kubectl delete pvc adguard-pvc-data -n adguard && \
sudo kubectl delete pv adguard-pv-conf -n adguard && \
sudo kubectl delete pv adguard-pv-data -n adguard && \
sudo kubectl delete namespace adguard
```

## Useful commands

Getting the pod name:
```sh
sudo kubectl get pods -n adguard
```

Getting an elaborate description of the pod (e.g. for troubleshooting):
```sh
sudo kubectl describe pods POD_NAME -n adguard
```
**NB:** `POD_NAME` is a placeholder for a unique pod ID, so you will have to replace it.

<br>


Getting the pod service(s) (e.g. IP and port(s) for the web UI etc.):
```sh
sudo kubectl get svc adguard-service -n adguard
```

Getting the `PersistentVolume`:
```sh
sudo kubectl get pv adguard-pv -n adguard
```

Getting the `PersistentVolumeClaim`:
```sh
sudo kubectl get pvc adguard-pvc -n adguard
```

Getting the `ConfigMap`:
```sh
sudo kubectl get configmap adguard-configmap -n adguard
```

Scaling the deployment:
```bash
sudo kubectl scale deployment DEPLOYMENT_NAME --replicas=0 # "pauses" the deployment
sudo kubectl scale deployment DEPLOYMENT_NAME --replicas=ORIGINAL_COUNT # starts the deployment again
```
**NB:** `ORIGINAL_COUNT` is only a placeholder for a number, so you will have to replace it. The default is `1`.

<br>

Rolling restart (allows you to update pods in the cluster gradually, to maintain service availability):
```bash
sudo kubectl rollout restart deployment DEPLOYMENT_NAME
```