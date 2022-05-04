# ejercicio-kubernetes
Exercise: mount web service on kubernetes

# Build app

    cd app
    docker build -t devops-app .
    docker run -p 5000:5000 devops-app


# Run on minikube

First start the minikube server, and then procede with the following:

    
    cd kubernetes
    kubectl apply -f secrets/secret-values.yaml
    kubectl apply -f deployments/devops-app.yaml
    kubectl apply -f hpa/devops-app-hpa.yaml
    kubectl apply -f services/devops-service.yaml
    minikube addons enable ingress
    kubectl apply -f ingress/devops-ingress.yaml

Then run ´minikube ip´ and open it on web browser. The app should be displayed.
