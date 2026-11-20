# Week 11 DevOps Lab

This repository contains the Week 11 containerization and Kubernetes lab files.

## Part I — Docker image

```powershell
cd lab11-Docker
docker run --rm hello-world
docker build --tag hellodocker .
docker image ls hellodocker
docker run --rm --name hellodocker-lab -d -p 4000:80 hellodocker
curl.exe http://localhost:4000
docker stop hellodocker-lab
docker container ls
```

The app says `Hello Pritesh!`, shows its container hostname, and displays the Redis fallback because this lab does not start a Redis server.

## Part II — NGINX on Minikube

Start Docker Desktop and Minikube, then run:

```powershell
kubectl apply -f k8/nginx-deploy.yaml
kubectl apply -f k8/nginx-service.yaml
kubectl rollout status deployment/nginx
kubectl get pods -l app=nginx -o wide
kubectl get svc nginx-nodeport
```

The service uses NodePort `30080`. On Windows with Minikube's Docker driver, `minikube service nginx-nodeport --url` may require its terminal to remain open. A reliable local check is:

```powershell
kubectl port-forward service/nginx-nodeport 8080:80
# In a second PowerShell window:
curl.exe -I http://localhost:8080
```

Cleanup:

```powershell
kubectl delete -f k8/nginx-deploy.yaml
kubectl delete -f k8/nginx-service.yaml
```

See `Week11-DevOps-Lab-Report.docx` and `.pdf` for the command descriptions and observed results. The `evidence` folder is reserved for original terminal screenshots captured by the student.
