# Kubernetes Architecture: Worker and Master Nodes Processes.

The Kubernetes architecture is made up of 3 processes which must be running on a Worker  Node and 4 Processes which need to be running on a Master Node called Master Processes to have a Kubernetes cluster. Basically, a Kubernetes cluster is made up of multiple nodes, but there are solutions to running a single node cluster,  Minikube is one of the solutions to having a single node cluster, but we are not getting into that today, so let’s focus on the main topic we are to talk about.

Let’s start with the Worker Processes, which are; **running an independent container runtime, Kubelet and Kube proxy**.

### **A container runtime.**

Since an application’s pod is running a container inside of it, every node must have an independent container runtime running on it.

### **Kubelet**

This is the process which actually schedules a pod and the containers running inside them. And this is a Kubernetes process itself, unlike a container runtime which is separate, and this Kubelet has an interface which it uses to interact with both the container and the Node. It basically takes a configuration and starts a pod with a container inside and assigns resources from the node to the container, like CPU, ram and storage resources.

### **Kube proxy.**

Pods communicate with each other using a service, which is like a load balancer that catches a request and forwards it to the pod it is directed to. And the process that’s actually responsible for the forwarding of these requests is actually the Kube proxy.

So now, how do we personally interact with our cluster? Like scheduling and rescheduling pods, monitoring or joining a new node. These are all done by our master node.

Now let's get into Kubernetes Master processes.

Mainly, every cluster has master and worker nodes, the master node is what we use for interacting with our cluster and our worker nodes are where our components are being created.

A master node has 4  processes running on it, which are our master processes, now let’s talk about them.

### **API Server.**

The API Server is where we send requests when interacting with our cluster like deployments requests for creating pods, and we can communicate with the API Server using either, a CLI, GUI or an API. The API server is like the cluster gateway to which we send requests.

### **Scheduler.**

A scheduler schedules a pod or any other component we have requested, after we send our request to the API Server, the API Server will send the request to the scheduler to schedule the component we have requested, and the scheduler will use its mechanism to decide on a specific worker node the component is to be created on, for example, checking for which worker node is less busy and has more resources. So basically, the scheduler just decides on which node a pod should be created, then makes a request to Kubelet to create the pod and the container inside of it.

### **Controller Manager.**

This process is what detects the current state of our cluster like when a pod dies, the controller manager will notice that and send a request to the scheduler to reschedule that pod. It is basically in charge of monitoring the state of the cluster and making sure our cluster is in the right state which we have configured it to be.

### **ETCD**

This is a key value store which is like our cluster brain, it stores and carries the current state of our cluster, like when a new pod or any other component is created,  then that update will be stored in our etcd.  And every other process works because of the etcd. For example, when a pod dies, the controller manager is going to know that only because the state of the cluster will be automatically updated in the etcd and the controller manager will get to know that our required state from our configuration is not the same with the current state of our cluster in the etcd, then it will send a request to the scheduler to reschedule that pod that died so that our cluster state will be the same with the state we have sent to our API Server as our required state.

Thanks for reading, and I hope to see you soon.

Please check later for more interesting and informative articles.