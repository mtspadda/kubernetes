# Kubernetes

## Getting to know Kubernetes

* **Vertical scaling:** Buy a more powerful machine to run more containers.
* **Horizontal scaling:** Add more machines to work in parallel with the original machine, and they will communicate with each other.

Kubernetes manages one or more machines together, which is called a cluster. Kubernetes can create and manage a cluster, and we can create a cluster on AWS, Azure, or GCS.

Kubernetes can determine the best machine to run the container, restart the container if it fails, and create another machine and run the container if necessary.

**This is called CONTAINER ORCHESTRATION**

## Creating a cluster

* **Beyond the basics:** Kubernetes goes beyond the orchestrator, encapsulating containers (a pod). Using Kubernetes resources, it can manage the architecture of an application.

**Master:** Coordinate and manage the cluster (CONTROL PANE)
    * Keep the pod running
    * Receive commands to manage the cluster
    * API
    * CONTROLLER MANEGER
    * SCHEDULER
    * ETCD

**Node:** Executes the application (NODES)
    * KUBELET
    * K-PROXY

**The API is responsible for maintaining communication between the control pane and the nodes.**

**This is where KUBECTL comes in:** Create, read, update, and delete resources.

## Creating and understanding pods

* A pod can contain one or more containers.
* Every time a pod is created, it is assigned an IP address.

[Image of Two containers sharing the same IP address but with different ports]

**PODS ARE EPHEMERAL! PODS DO NOT REBORN!**
    * Without containers, the pod will be gone.
* Communication is much easier between containers in the same pod because they are LOCALHOST.

**kubectl run nginx-pod --image=nginx:latest**

**kubectl get pods**

**kubectl get pods --watch #this shows any updates to the pods**

**kubectl describe <name> #describes what is going on and other information/errors when mounting the pods**

**kubectl edit pods <name> #opens a notepad and allows you to edit pod settings**

**kubectl delete pod <name> #kills the pod**

**kubectl delete -f \\.first-pod-clareted #also kills the pod, by the definition file**

**kubectl exec -it <name> -- <command> #enters the pod through the pod's bash**

## Exposing pods with services

**SERVICES**

* Abstraction to expose applications running on one or more pods
* Provide fixed IP addresses for communication
* Provide a DNS for one or more pods
* Are capable of load balancing

**4.04: ClusterIP**

* The service is not a two-way street. It is linked to the pod. In the example, it will be linked to pod-2.
* The pods: pod-1 and news-portal must access the service before accessing pod-2, and this is possible through LABELS. The service is informed that it only accesses resources with the desired label.
* Killing the pod does not kill the service. It is left without a place to dispatch the messages.

**4.06 Creating a NodePort**

* It is a type of service that allows communication with the outside world.
* It also functions as a clusterIP.

**4.08 Creating a Load Balancer**

* It is like a nodePort, but it integrates with the load balancer of the cloud provider you choose.
* You need to create the pod and the service in the cloud.
* It is possible to view the services in the cloud. After published on AWS/GCP/Azure, you can access it through the browser.

## Additional resources

* Kubernetes documentation: [https://kubernetes.io/docs/home/](https://kubernetes.io/docs/home/)
* Kubernetes tutorials: [https://kubernetes.io/docs/tutorials/](https://kubernetes.io/docs/tutorials/)
* Kubernetes community: [https://kubernetes.io/community/](https://kubernetes.io/community/)

## Conclusion

Kubernetes is a powerful tool that can help you manage and scale your containerized applications. By understanding the basics of Kubernetes, you can get started with using it to deploy your applications.
