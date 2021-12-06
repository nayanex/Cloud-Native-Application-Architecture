### Get deployments
`kubectl get deploy`

### Get Replicas
`kubectl get rs`

### Get Pods
`kubectl get po`

`kubectl get po -n test-udacity`

### Get Nodes
`kubectl get no`

### Get ConfigMaps
`kubectl get cm`

### Get Secrets
`kubectl get secrets`

### Create Deployment
`kubectl create deploy go-helloworld --image=pixelpotato/go-helloworld:v1.0.0`

`kubectl port-forward po/go-hellowworld-fcd468f98-zjvlg 6111:6111`

> Where go-hellowworld-fcd468f98-zjvlg is the name of the pod which host the container
> You can access the application going to 127.0.0.1:6111

### Edit deployment
`kubectl edit deploy go-helloworld -o yaml`

> You can, for example, change the image version

### Deleting a namespace
`kubectl delete namespaces <insert-some-namespace-name>`

### Create a namespace
`kubectl create ns demo --dry-run=client -o yaml > namespace.yaml`

### Label a resource
`kubectl label deploy nginx-alpine tag=alpine --namespace demo`

`kubectl label ns demo tier=test`

### create the nginx-alpine deployment 
`kubectl create deploy nginx-alpine --image=nginx:alpine  --replicas=3 --namespace demo`

### label the deployment
`kubectl label deploy nginx-alpine app=nginx tag=alpine --namespace demo`

### expose the nginx-alpine deployment, which will create a service
`kubectl expose deployment nginx-alpine --port=8111 --namespace demo`

> expose the `go-helloworld` deployment on port 8111

### note: the application is serving requests on port 6112
`kubectl expose deploy go-helloworld --port=8111 --target-port=6112`

`kubectl run test-$RANDOM --namespace=default --rm -it --image=alpine -- sh`

`wget -qO- 10.98.151.167:6112 `

### create a config map
`kubectl create configmap nginx-version --from-literal=version=alpine --namespace demo`

### create a Configmap to store the color value
`kubectl create configmap test-cm --from-literal=color=yellow`

### create a Secret to store the secret color value
`kubectl create secret generic test-secret --from-literal=color=blue`

`kubectl describe secrets test-secret`

`kubectl get secrets test-sec -o yaml`

`echo "cmVk" | base64 -D`

### Get Logs
`kubectl logs RESOURCE/NAME [FLAGS]`

### Delete Resources
`kubectl delete RESOURCE NAME`
