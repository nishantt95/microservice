# Microservice

The project is split into three parts:
1. [The Simple Frontend](/frontend)
A basic Ionic client web application which consumes the RestAPI Backend. 
2. [The RestAPI Feed Backend](/feed-service), a Node-Express feed microservice.
3. [The RestAPI User Backend](/user-service), a Node-Express user microservice.

## Getting Setup
Command to deploy this project on kubernetes cluster. Change directory to `./deployment/k8s`
```angular2
kubectl apply -f aws-secret.yaml -f env-configmap.yaml -f env-secret.yaml
kubectl apply -f backend-feed-service.yaml -f backend-user-service.yaml -f frontend-service.yaml -f reverseproxy-service.yaml
kubectl apply -f backend-feed-deployment.yaml -f backend-user-deployment.yaml -f frontend-deployment.yaml -f reverseproxy-deployment.yaml
```

Container for each service on docker hub.
```angular2
nishantt95/rest-user
nishantt95/rest-feed
nishantt95/reverse-proxy
nishantt95/frontend
```
Building docker images
```angular2
docker-compose -f deployment/docker/docker-compose-build.yaml build --parallel
```

Running project on local system. Please set environment variable on your local system.
```export POSTGRESS_USERNAME=***;
   export POSTGRESS_PASSWORD=***;
   export POSTGRESS_DB=***;
   export POSTGRESS_HOST=***;
   export AWS_REGION=us-east-1;
   export AWS_PROFILE=***;
   export AWS_BUCKET=***;
   export JWT_SECRET=helloworld;
```

Change directory to `./deployment/docker` and run `docker-compose up` and now the application will be available at `http://localhost:8100/`

## Development process view
All the pods running inside kubernetes (AWS Elastic Kubernetes Service)

![Alt text](/screenshots/get-pods.PNG?raw=true")


####Port forwarding 

- Reverse proxy

![Alt text](/screenshots/kubectl-port-forward-reverseproxy.PNG?raw=true")


- Frontend

![Alt text](/screenshots/kubectl-port-forward-frontend.PNG?raw=true)

#### Application View

- Before login

![Alt text](/screenshots/application-view-1.PNG?raw=true)


- After login and uploading new image

![Alt text](/screenshots/application-view-2.PNG?raw=true)


#### Travis CI build success

![Alt text](/screenshots/travis-ci-1.PNG?raw=true)

![Alt text](/screenshots/travis-ci-2.PNG?raw=true)


#### Running docker on local system

![Alt text](/screenshots/running-docker-local.PNG?raw=true)
