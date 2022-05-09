# alert-manager-dashboard-setup

### Run Docker image locally:

```bash
docker run -p 8080:8080 --net=host -e ALERTMANAGER_URI=http://localhost:9093 ghcr.io/prymitive/karma:latest
```

### To Run in Kubernetes

```bash
kubectl apply -f mainfest.yaml
```
