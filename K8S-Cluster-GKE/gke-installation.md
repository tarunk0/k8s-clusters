# K8S Cluster Using GKE:
  - Installation
  - Testing
  
  #### In GKE Cluster we don't get access to the master node. The master node is just created and managed by Google Cloud only. We can access our cluster using the Cloud Shell which is a free service provided by GCP. Also we can connect our cluster to any other machine using the kube config file. 
  
  ## Step: 1 (Using-GUI)
 - Login to google cloud and create the cluster. 
 - Connect to cluster using cloudshell or local machine using kube config. 
     
  ```sh
     kubectl get nodes -o wide
     kubectl get all
 ```
 ## Step: 2 (Alternative) (Using - Command Line)
 
  - You can use the command line or cloud shell to create the cluster using the following commands
    
 ```sh
    gcloud config set project <project-name>
    gcloud config set compute/zone <your-zone>
    #the above commands set the default zone and project for your cluster
 ```
  - Creating the cluster.
    
 ```sh
    gcloud container clusters create <name-of-cluster> --num-nodes=<no-of-nodes-you-want>
    gcloud container clusters get-credentials <name-of-cluster>
    #This command configures the kubectl to use your cluster
 ```
 
