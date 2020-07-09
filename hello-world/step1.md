This is your first step.

## Task

Let’s deploy our first app on Kubernetes with the `kubectl create deployment` command.
We need to provide the deployment name _kubernetes-bootcamp_ and app image location via `--image` (include the full repository url for images hosted outside Docker hub).

`kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1`{{execute}}

Great! You just deployed your first application by creating a deployment. This performed a few things for you:
  - searched for a suitable node where an instance of the application could be run (we have only 1 available node)
  - scheduled the application to run on that Node
  - configured the cluster to reschedule the instance on a new Node when needed

To list your deployments use the get deployments command:

`kubectl get deployments`{{execute}}

We see that there is 1 deployment running a single instance of your app. The instance is running inside a Docker container on your node.

`kubectl get pods`{{execute}}

To provide redundancy for our app we want to increase the number of running app instances. 
We can use the `kubectl scale` command with the parameter `--replicas` to to scale our app to three instances.

`kubectl scale deployment/kubernetes-bootcamp --replicas=3`{{execute}}

By running the deployments command again, we can validate that our deployment has now three running instances instead of one.

`kubectl get deployments`{{execute}}

To list the actual pods that are running the app containers, we can issue the following command:

`kubectl get pods`{{execute}}

We should see three running pods.
The name of the pods is a compound of the deployment name, the replicaset random string and a randomly generated string.
What happened behind the scenes is that Kubernetes automatically created a ReplicaSet for us when we created the deployment.
The ReplicaSet is responsible for managing the state of our desired three replicas for the application.
To list the replica set and see that the name comes from it, we can use the following command:

`kubectl get replicasets`{{execute}}

Now let's try to kill one of the pods and observe K8s self-healing functionality.
First, extract one of the pods' names (or in a environment variable).

`export POD_NAME=$(kubectl get pods -o jsonpath="{.items[0].metadata.name}")
echo Name of the Pod: $POD_NAME`{{execute}}

Kill the pod via the following command (replace with your preferred pod name or use the env variable).
`wait=false`is just there to free the terminal so you can immediately check the self-healing with the next command!

`kubectl delete pods $POD_NAME --wait=false`{{execute}}

Now observe that a new pod was automatically created to make it three running instances again as desired:

`kubectl get pods`{{execute}}

If you are fast enough, you can see one pod with status Terminating (the one, we just killed) and one with status ContainerCreating that was immediately scheduled as a replacement.
If you are a little late and the new pod is already up, closely observe the age of the pods, so you can see that one was just recently created.
