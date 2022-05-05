# ejercicio-kubernetes
Exercise: mount web service on kubernetes

# Build app

``` shell
cd app
docker build -t devops-app .
docker run -p 5000:5000 devops-app
```



# Run on minikube

First start the minikube server, and then procede with the following:

``` shell
cd kubernetes
kubectl apply -f secrets/secret-values.yaml
kubectl apply -f deployments/devops-app.yaml
kubectl apply -f hpa/devops-app-hpa.yaml
kubectl apply -f services/devops-service.yaml
minikube addons enable ingress
kubectl apply -f ingress/devops-ingress.yaml
```
    
    
## Building the image so it can be used within minikube
Minikube downloads images from Dockerhub by default. If no image is pulled, the deployment won't work. We need to build the image within a minikube environment and set some params on the deployment.

1. Configure the deployment for local images
   - Put `imagePullPolicy: Never` config in the containers part of the config.
   - Set `image` config to the same name as the locally built image
2. Build the image
   ```shell
   eval $(minikube docker-env)
   docker build -t my_image .
   ```

Then run `minikube ip` and open it on web browser. The app should be displayed.
