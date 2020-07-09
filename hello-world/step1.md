This is your first step.

## Task

This is an _example_ of creating a scenario and running a **command**

TODO scale to 3 should be an extra step
`kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1 --replicas=3`{{execute}}

`kubectl get deployments`{{execute}}

`kubectl get pods`{{execute}}

`export POD_NAME=$(kubectl get pods -o jsonpath="{.items[0].metadata.name}")
echo Name of the Pod: $POD_NAME`{{execute}}

`kubectl delete pods $POD_NAME`{{execute}}

`kubectl describe deployments`{{execute}}
