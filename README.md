## What is Kubernetes?
- Kubernetes, often abbreviated as “K8s”, orchestrates containerized applications to run on a cluster of hosts. 
- Kubernetes is an open-source platform which automates the deployment and management of cloud native applications using on-premises infrastructure or public cloud platforms. 
- Kubernetes automates the vital aspects of container lifecycle management, including scaling, replication, monitoring, and scheduling.
- Some Extra points:
   - CNCF Graduated.
   - Born Outof Borg and Omega.
   - Launched in 2014. 
   - Designed for Scale.
   - Run anywhere. 

## Why Kubernetes?
 - Few containersa are fine but what about if we have millions of them?
 - How to monitor them?
 - What about solving the problem of overloading a single node? What about running the containers on Various nodes?
 - Autoscaling if we just need to spill out or spill in desired containers. That too automatically.
 - Scheduling. 
 - Self Healing Capabilities. 
 
   ![image](https://user-images.githubusercontent.com/92631457/186976107-1707e5e8-8e14-4d6d-ba31-440a6478c439.png)

   ![image](https://user-images.githubusercontent.com/92631457/186976408-c230a884-f19d-49ac-8907-791a17d53e53.png)



 
## Kubernetes Architecture:
 ![image](https://user-images.githubusercontent.com/92631457/186917158-700707f4-9ecf-4bb5-aeda-2e12d571152e.png)
 
 ![image](https://user-images.githubusercontent.com/92631457/186975827-2bb0e3dc-c8da-4c56-8512-286c7b778a10.png)
  
   Kubernetes follows a client-server architecture. It’s possible to have a multi-master setup (for high availability), but by default there is a single master server which acts as a controlling node and point of contact. The master server consists of various components including a kube-apiserver, an etcd storage, a kube-controller-manager, a cloud-controller-manager, a kube-scheduler, and a DNS server for Kubernetes services. Node components include kubelet and kube-proxy on top of Docker.

### Master Components:
  ### Etcd: 
  -  It is a simple, distributed key value storage which is used to store the Kubernetes cluster data (such as number of pods, their state, namespace, etc),   API objects and service discovery details. 
  -  It is only accessible from the API server for security reasons. 
  -  Etcd enables notifications to the cluster about configuration changes with the help of watchers. Notifications are API requests on each etcd cluster node to trigger the update of information in the node’s storage.
  
  ### Kube-API-Server:
   - Kubernetes API server is the central management entity that receives all REST requests for modifications (to pods, services, replication sets/controllers and others), serving as frontend to the cluster. 
   - Also, this is the only component that communicates with the etcd cluster, making sure data is stored in etcd and is in agreement with the service details of the deployed pods.
  
  ### Kube-Controller-Manager:
  
   - It runs a number of distinct controller processes in the background (for example, replication controller controls number of replicas in a pod, endpoints controller populates endpoint objects like services and pods, and others) to regulate the shared state of the cluster and perform routine tasks. 
   - When a change in a service configuration occurs (for example, replacing the image from which the pods are running, or changing parameters in the configuration yaml file), the controller spots the change and starts working towards the new desired state.
  
  ### Kube-Schedular:
   - It helps schedule the pods on the specific nodes as per it's resource utilization. 
   - For example, if the application needs 1GB of memory and 2 CPU cores, then the pods for that application will be scheduled on a node with at least those resources. 
   - The scheduler runs each time there is a need to schedule pods. The scheduler must know the total resources available as well as resources allocated to existing workloads on each node.   
   
### Node Components:
Below are the main components found on a (worker) node:

   ### Kubelet: 
   - Kubelet is the main service on the node. It tracks the state of a pod to ensure that all the containers are running in the desired state and are healthy. 
   - It provides a heartbeat message every few seconds to the control plane. If a replication controller does not receive that message, the node is marked as unhealthy.
   
   ### Kube-Proxy:
   - The Kube proxy routes traffic coming into a node from the service. It forwards requests for work to the correct containers.
   - It also assigns the IP to the pod and manages all the networking part. 


## Real World Examples:
  ### Pinterest’s Kubernetes Story:
   - With over 250 million monthly active users and serving over 10 billion recommendations every single day, the engineers at Pinterest knew these numbers are going to grow day by day, and they began to realize the pain of scalability and performance issues.

   - Their initial strategy was to move their workload from EC2 instances to Docker containers; they first moved their services to Docker to free up engineering time spent on Puppet and to have an immutable infrastructure.
   - The next strategy was to move to Kubernetes. Now they can take ideas from ideation to production in a matter of minutes, whereas earlier they used to take hours or even days. They have cut down so much overhead cost by utilizing Kubernetes and have removed a lot of manual work without making engineers worry about the underlying infrastructure.

### The New York Times’s Journey to Kubernetes:
   - Today the majority of the NYT’s customer-facing applications are running on Kubernetes. What an amazing story. The biggest impact has been an increase in the speed of deployment and productivity. Legacy deployments that took up to 45 minutes are now pushed in just a few. It’s also given developers more freedom and fewer bottlenecks. The New York Times has gone from a ticket-based system for requesting resources and weekly deploy schedules to allowing developers to push updates independently.

### Tinder’s Move to Kubernetes:
   - Due to high traffic volume, Tinder’s engineering team faced challenges of scale and stability. What did they do?
   - The answer is, of course, Kubernetes.
   - Tinder’s engineering team solved interesting challenges to migrate 200 services and run a Kubernetes cluster at scale totaling 1,000 nodes, 15,000 pods, and 48,000 running containers.
   - Was that easy? No way. However, they had to do it for the smooth business operations going further. One of their engineering leaders said, “As we onboarded more and more services to Kubernetes, we found ourselves running a DNS service that was answering 250,000 requests per second.” Tinder’s entire engineering organization now has knowledge and experience on how to containerize and deploy their applications on Kubernetes.

![image](https://user-images.githubusercontent.com/92631457/186980609-32ccbf87-47a5-4932-8ed1-4395a5d7f5d3.png)





