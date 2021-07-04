# kubernetes

`kubectl get nodes`  
`kubectl get deployments`

`kubectl get pods`  
`kubectl describe pods`

### use an HTTP proxy to access the Kubernetes API
`kubectl proxy`  
`export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')`  
`echo Name of the Pod: $POD_NAME`  
`curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/`

### Access logs
`kubectl logs $POD_NAME`

### Run commands in a container
`kubectl exec $POD_NAME -- env`  
`kubectl exec -ti $POD_NAME -- bash`  
`kubectl exec -ti $POD_NAME -- curl localhost:8080`

## Services

`kubectl get services`

`kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080`  
`kubectl describe services/kubernetes-bootcamp`

`export NODE_PORT=$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')`  
`echo NODE_PORT=$NODE_PORT`

`curl $(minikube ip):$NODE_PORT`


`kubectl describe deployment`  
`kubectl get pods -l app=kubernetes-bootcamp`  
`kubectl get services -l app=kubernetes-bootcamp`

`export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')`  
`echo Name of the Pod: $POD_NAME`

### Apply new label

`kubectl label pods $POD_NAME version=v1`  
`kubectl describe pods $POD_NAME`

#### Query pods using new label

`kubectl get pods -l version=v1`

### Delete a service

`kubectl delete service -l app=kubernetes-bootcamp`

## Scale a deployment

`kubectl get deployments`

### See the replica set

`kubectl get rs`

### Scale

`kubectl scale deployments/kubernetes-bootcamp --replicas=4`  
`kubectl get deployments`  
`kubectl get pods -o wide`

### View a deployments event logs

`kubectl describe deployments/kubernetes-bootcamp`