This is your first step.

## Task

This is an _example_ of creating a scenario and running a **command**

`kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1`{{execute}}

`kubectl get deployments`{{execute}}

`kubectl get pods`{{execute}}

`kubectl scale deployment/kubernetes-bootcamp --replicas=3`{{execute}}

`kubectl get deployments`{{execute}}

`kubectl get pods`{{execute}}

`export POD_NAME=$(kubectl get pods -o jsonpath="{.items[0].metadata.name}")
echo Name of the Pod: $POD_NAME`{{execute}}

`kubectl delete pods $POD_NAME`{{execute}}

`kubectl get pods`{{execute}}
