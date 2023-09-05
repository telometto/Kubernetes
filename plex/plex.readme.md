# Deployment
---
## How to deploy
```sh
sudo kubectl apply -f plex-namespace.yml && \
sudo kubectl apply -f plex-pv.yml && \
sudo kubectl apply -f plex-pvc.yml && \
sudo kubectl apply -f plex-configmap.yml && \
sudo kubectl apply -f plex-deployment.yml && \
sudo kubectl apply -f plex-service.yml
```

## How to destroy
```sh
sudo kubectl delete service plex-service -n plex && \
sudo kubectl delete deployment plex-deployment -n plex && \
sudo kubectl delete configmap plex-config -n plex && \
sudo kubectl delete pvc plex-pvc-config -n plex && \
sudo kubectl delete pvc plex-pvc-movies -n plex && \
sudo kubectl delete pvc plex-pvc-series -n plex && \
sudo kubectl delete pvc plex-pvc-other-media -n plex && \
sudo kubectl delete pv plex-pv-config -n plex && \
sudo kubectl delete pv plex-pv-movies -n plex && \
sudo kubectl delete pv plex-pv-series -n plex && \
sudo kubectl delete pv plex-pv-other-media -n plex && \
sudo kubectl delete namespace plex
```

## Useful commands
Will update this when I'm not lazy 😜