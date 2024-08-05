# Source code

This folder contains a simple containerized Go web application.

```bash
#Use docker to build the webapp locally
docker build . -t webapp:v1
```

```bash
#Run the webapp locally
docker run --rm -p 8080:8080
```

```bash
#Tag the webapp with an Azure Container Registry name
docker tag webapp:v1 <acrName.azurecr.io>/webapp:v1
```

```bash
#Log into ACR
az acr login
````

```bash
#Push the container image to ACR
docker push <acrName.azurecr.io>/webapp:v1
```
