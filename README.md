# ejercicio-kubernetes
Ejercicio: montar web service en kubernetes

# Build app

    cd app
    docker build -t devops-app .
    docker run -p 5000:5000 devops-app

