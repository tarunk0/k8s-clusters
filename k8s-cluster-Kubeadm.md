
## Creation of Kubernetes Cluster using Kubeadm:
 - Installation.
 - Testing.

### Installation:
 
  ## Step: 1
   - Launch three instances in AWS/GCP, one for master node and other two for the worker nodes. Although you can make any number of master or nodes depending upon the requirements. If there are more than one master, then it's good for high availability.
     - Perform these steps on all the three nodes:
       - Installation of docker
  ```sh
     apt update
     apt install docker.io -y
     docker --version
     #start docker service
     systemctl start docker
     systemctl enable docker
  ```
  ![image](https://user-images.githubusercontent.com/92631457/186983499-8224822b-771e-4bd4-8840-3664184eaa37.png)

   - Since you are downloading Kubernetes from a non-standard repository, it is essential to ensure that the software is authentic. This is done by adding a signing key. Download it using the following:
 ```sh
    sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add 
 ```
   - Edit the source.list.d file and add the following repository:
 ```sh 
    vim /etc/apt/sources.list.d/kubernetes.list
    deb http://apt.kubernetes.io/ kubernetes-xenial main
    #copy it and :wq
 ```
   - Install the dependencies like kubelet, kubeadm,  kubectl, kubernetes-cni
 ```sh
    apt update
    apt install -y kubelet kubeadm kubectl kubernetes-cni
 ```
## Step: 2 Bootstrapping the Master node:
  ### Run the following command in master only and copy the code show in the last, starting from kubeadm join ...
  
  ```sh
     kubeadm init
  ```
  ![image](https://user-images.githubusercontent.com/92631457/186988957-ad72bf9f-dfca-44fd-922c-6837d507f94c.png)

  
  ```sh
     mkdir -p $HOME/.kube
     cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
     
     chown $(id -u):$(id -g) $HOME/.kube/config
     
     kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
     kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/k8s-manifests/kube-flannel-rbac.yml
  ```

 ## Step: 3 Just paste the long command like kubeadm join on to the worker nodes and you are done:
   - Start using the cluster fromt the master node using kubectl command line utility. 
   - After pasting the command you will see the out put like this:
    
    
   ![image](https://user-images.githubusercontent.com/92631457/186988419-032d63ba-560c-4b3d-a2e6-857e606d160e.png)
   
   
## Step: 4 Testing
   - On master node
 ```sh
    kubectl get all
    kubectl get nodes -o wide
 ```
 
   - Apply some deployment file on the cluster. 
 ```sh
    kubectl apply -f <file-name.yaml>
    kubectl apply -f <svc.yaml>
 ```
 ![image](https://user-images.githubusercontent.com/92631457/186996393-49f277dd-36df-4e0b-a12c-41f73e846681.png)
 
   - Make sure to make your service exposed using NodePort to make it accessible from outside. 
   - After you do that you will see the deployment on master, as well as worker nodes.
   - Check the screenshots. 

![image](https://user-images.githubusercontent.com/92631457/186996508-6e617ac2-3e3c-40f6-9f7b-aff27762c815.png)

![image](https://user-images.githubusercontent.com/92631457/186996561-06e4fbf4-424c-417e-a543-3a93ba66945b.png)


![image](https://user-images.githubusercontent.com/92631457/186996617-9df021f8-9803-4bde-a19c-4632af6d8e84.png)


   
