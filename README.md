Build image first `docker build -t kub-node-app .`

Create dockerhub repository `ashishyd/kub-node-app`

Change local image to this name `docker tag kub-node-app ashishyd/kub-node-app`

Push this to the repository `docker push ashishyd/kub-node-app`

# Kubernetes Imperative approach (without YAML files)
Kubernetes uses rolling update strategy

If minikube is running, then run kubernetes command (the images can only be pulled from the repository not locally)

To create a new deployment using imperative approach

`kubectl create deployment node-app --image=ashishyd/kub-node-app`

To check deployments

`kubectl get deployments`

To check Pods

`kubectl get pods`

Now to check the deployment on minikube, it will open automatically on browser

`minikube dashboard`

Create new service to expose the endpoint

`kubectl expose deployment node-app --type=LoadBalancer --port=8080`

Check services

`kubectl get services`

To run your container using minikube

`minikube service node-app`

To scale the deployment node

`kubectl scale deployment/node-app --replicas=3`

To lower the number of replicas

`kubectl scale deployment/node-app --replicas=1`

Very important is when you change the code and build a new image you have to add new tab as below, because kubernetes does not update image if its same tag
`docker build -t ashishyd/kub-node-app:v2 .`

set new image to kubernetes using `kubectl set image deployment/node-app kub-node-app=ashishyd/kub-node-app:v2`

to check status of the deployment rollout

`kubectl rollout status deployment/node-app`

To rollback the deployment

`kubectl rollout undo deployment/node-app`

To check rollout history

`kubectl rollout history deployment/node-app`

To rollback to specific version

`kubectl rollout undo deployment/node-app --to-revision=<revision_number>`

To delete a service

`kubectl delete service node-app`

To delete a deployment

`kubectl delete deployment node-app`

# Kubernetes Declarative Approach

To create a deployment

`kubectl apply -f=deployment.yaml`

To create a service

`kubectl apply -f=service.yaml`

Run `minikube service node-app-service` to see application on browser

To delete a deployment

`kubectl delete -f=deployment.yaml`

To delete a deployment and service

`kubectl delete -f=deployment.yaml -f=service.yaml`

You can also merge configuration in one file separated by `---`
Note: service configuration is first as it follows top down approach

