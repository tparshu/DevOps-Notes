Kubernetes
------------------------

Google created this kubernetes.
It is a opensource tool.
Pre-requisite is docker.

k8s  -- 8 letters between  k  and  s

It is a container orchestration tool.
 
Kubernetes creates cluster, deploy and manage clusters.

By using kubernetes we form a cluster
K8S schedules, runs and managers isolated containers.

Convert isolated containers running on different hardwares into a cluster.

In AWS we have a service EKS  ( Elastic kuberneters service )

Features of kubernetes
---------------------------------
1) Orchestration (  clustering any no of containers on different hardwares)
2) Auto scaling
3) Auto healing ( new containers in place of crashed containers 
                              similar to handling failover scenarios in docker swarm )
4) load balancing
5) rollback  ( going to previous versions )


Kubernetes Architecture
-------------------------------

Cluster is combination of 1 master and multiple nodes.

Pod is atomic unit of deployment in kubernetes.




Pod consists of one or more docker containers.
Pod runs on node.
Node is controlled by Kubernetes master


Kubernetes does not understand containers.


Kubernetes can understand only pods.


In this diagram , we have one master and one node.
node is also called minion.
Kubernetes master is also called as control plane.



++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


+++++++++++++++++++++++++++

Kubernetes Terminology
------------------------

In docker Swarm,  Manager machine takes the load.




In Kubernetes Manager is called as Master.


Kubernetes master does not take up the load. 


It only distributes load to slaves/ nodes.

Nodes are also called Minion.
Minions combined together is called as cluster.

Smallest Object that kubernetes can create is pod.

Within the pod, we have the container.

Kubernetes commands are always triggered using kubectl.

Kubernetes introduced on June 2014 by Google.

To practice Kubernetes on AWS , we have a service EKS ( Elastic Kubernetes Service )
To practice Kubernetes on Azure , we have a service AKS ( Azure Kubernetes Service )
To practice Kubernetes on GCP , we have a service GKE ( google Kubernetes engine )

AWS, is expensive
Freeways to work on kubernetes is katakoda
Goto https://www.katacoda.com/  
Learn --- --- Kubernetes Introduction -- Start Course
-- Launch Multinode cluster  -- Start Scenario

Login using gmail

Step 1: Initialise Master
Run kubeadm init command ( just click on it )

We need to copy configuration files to home directory and change ownership.

Run sudo cp command.

Continue

Step 2: Deploy Container networking Interface
Run the three commands
cat  , kubectl  apply, kubectl  get pod

Continue

Step 3:  
Run
kubeadm  token list

kubeadm join   ( this will create slave )

Continue
Step 4: 
Run
kbectl  get nodes
You can see one controlplane and one node

We have one more site
https://labs.play-with-k8s.com/

using which we can practice  Kubernetes.

But, both the options will be slow.

++++++++++++++++++++++++++++++++
We learn kuberntes on GCP, as AWS is expensive.

Sign up to GCP account using gmail credentials. ( Free trial comes with USD 300 )

https://cloud.google.com/
Sign in using gmail

Click on console
You will enter into google cloud platform console
Navigation Menu --- Kubernetes Engine --  Clusters -- Create cluster --  Create

Observation: Cluster size is 3
By default, it creates 3 node cluster.


Master Machine is not provided as alinux server.
It is given as a service.
As it is a service, it never fail.
So, we do not need to worry about master.

To connect to the cluster
-------------------------------
In GCP, Cloud Shell is the terminal, used to connect to the cluster.

kubectl get nodes    ( we can see the nodes )

After practice,  Delete the cluster.
Next day,  we can create the cluster again.
-----------------------





Kuberntes uses various types of objects.

1 Pod:  This is a layer of abstraction on top of a container. 
This is the smallest object that kubernetes can work on. 
In the pod, we have the container. 
kubectl commands will work on the pod and pod communicates there instructions to the container.


2. Service Object: This is used for port mapping and network load balancing.


3. NameSpace: This is used for creating partitions in the cluster. Pods running in  a namespace cannot communicate with other pods running in other namespace.




4. Secrets: This is used for passing encrypted data to the pods.



5. ReplicaSet / Replication COntroller: This is used for managing multiple replicas of a pod to perform activities like 
load balancing and autoscaling.

6. Deployment: This is used for performing all activites that a ReplicaSet can do. It can also handle rollling updates.

Create Cluster.
Open cloud shell terminal.

Command to create a pod
-----------------------------

 kubectl run --image tomcat   webserver

( Webserver is pod name )




To see list of pods
------------------------
kubectl get pods

If we do not specify replicas, it creates only one replica.

To delete the pod
--------------------
kubectl delete pods webserver


Lets create pod again
-----------------------
 kubectl run --image tomcat webserver

To know on which node, this pod is running




kubectl get pods -o wide
( o - stands for output )

-------------------------
But, Kubernetes performs container orchestration by using definition files. Definition files are yml files 

Definition file, will have 4 top level elements

1. apiVersion:
2. kind:
3. metadata:
4. spec: 


apiVersion:
---------------
Depending on kubernetes object we want to create, there is corresponding code library we want to use.

apiVersion referes to code library

Kind     			apiVersion
========================
Pod       			v1
Service   			v1
NameSpace     			v1
Secrets         		v1
RepliaSet       		apps/v1
Deployment      		apps/v1










kind:
----------
Refers to kubernetes object which we want to create.
Ex: Pod, Replicaset, service etc

metadata:
-----------
Additional information about the kubernets object
like name, labels  etc

spec:
------
Contains docker container related information like image name,
 environment variables, port mapping etc.


+++++++++++++++++++++++++++++++++++++++++

Connect to cluster by using cloud shell.

$ mkdir samplefiles




Ex1:  Create a pod definition file to start nginx in a pod. 
Name the pod as nginx-pod, name the container as appserver. 




vi pod-definition1.yml

---
apiVersion: v1
kind: Pod
metadata:
 name: nginx-pod
 labels:
  author: sunil
  type: reverse-proxy
spec:
 containers: 
  - name: appserver
    image: nginx

:wq






Command to run the definition file
------------------------------------------
kubectl create -f pod-definition1.yml


Pod is created.






To get the list of pods
---------------------------
kubectl get pods


To get the list of pods along with IP address  and which node the pod is running
---------------------------
kubectl get pods -o wide  


To delete the pod created from the above file
---------------------
kubectl delete -f  pod-definition1.yml


++++++++++++++++++++++++++++++++++






 ++++++++++++++++++++++++++++++++++
ReplicationController:
This is an high level object used for handling multiple replicas of a specific pod. Here we can perform load balancing and scalling.

ReplicationController uses keys like replicas, template etc in the "spec" section.

In template section we can give metadata related to the pod and also use another spec section where we can give containers information.

Ex: Create  a replication controller for creating 3 replicas of httpd



vi  replication-controller.yml


---
apiVersion: v1
kind: ReplicationController
metadata:
 name: httpd-rc
 labels:
  author: sunil
spec:
 replicas: 3
 template:
  metadata:
   name: httpd-pod
   labels:
    author: sunil
  spec:
   containers:
    - name: myhttpd
      image: httpd
      ports:
       - containerPort: 80
         hostPort: 8080


:wq


kubectl delete --all pods   ( To delete all the existing pods )

kubectl  get pods  ( No pods available )

Open the port
-------------------
  gcloud compute firewall-rules create rule21 --allow tcp:8080




  kubectl create -f replication-controller.yml

 kubectl  get pods  ( We should get 3 pods )

 kubectl  get pods -o wide ( Observation , 3 pods are distributed in 3 nodes )

  kubectl  get nodes -o wide


Take external IP ( Public IP )  of any node
34.132.28.9:8080

34.28.177.155:8080




To delete the replicas
  kubectl delete -f replication-controller.yml


++++++++++++++++++++++++++
ReplicaSet
---------------

Pod is the smallest kubernetes object, which we worked on.

  Next Level is replication controller.


    ReplicaSet is similar to replication controller.



   In replicatSet, we have an additional field in spec section called as "selector" field.



This selector uses a child element called "matchLabels"   , where it will search for pods based on a 
specific label name, and adds them to the cluster.

Ex: Create a replicaset file to start 4 tomcat replicas and then perform scaling  

vi replica-set.yml



---
apiVersion: apps/v1
kind: ReplicaSet
metadata:
 name: tomcat-rs
 labels:
  type: webserver
  author: sunil
spec:
 replicas: 4
 selector:
  matchLabels:
   type: webserver
 template:
  metadata:
   name: tomcat-pod
   labels:
    type: webserver
  spec:
   containers:
    - name: mywebserver
      image: tomcat
      ports:
       - containerPort: 8080
         hostPort: 9090

 
:wq


kubectl create -f replica-set.yml


kubectl  get pods  ( We should get 4 pods )

  kubectl  get replicaset

Lets perform scaling from 4 pods to 6 pods

Option 1: We can open the definition file and make changes in the code from 4 to 6 in replicas field.

vi replica-set.yml

Now, we should not use create commands, we should use replace command.

kubectl replace -f replica-set.yml

kubectl  get pods  ( We should get 6 pods )

Option 2: 

kubectl scale --replicas=2 -f replica-set.yml

kubectl  get pods  ( We should get 2 pods )

 
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++


Deployment Object
-------------------------
This is also an high level object which can be used for scalling, load balancing and perform rolling updates.

Create a deployment file to run nginx 1.7.9 with 3 replicas. 
Later perform a rolling update to nginx 1.9.1 


vi deployment.yml
---
apiVersion: apps/v1
kind: Deployment
metadata:
 name: nginx-deployment
 labels:
  author: sunil
  type: proxyserver
spec:
 replicas: 3
 selector:
  matchLabels:
   type: proxyserver
 template:
  metadata:
   name: nginx-pod
   labels:
    type: proxyserver
  spec:
   containers:
    - name: nginx
      image: nginx:1.7.9
      ports:
       - containerPort: 80
         hostPort: 8888
 

:wq

kubectl get all  ( we have one   default service running )

kubectl create -f deployment.yml

TO check, if the deployment is created or not
--------------------------------------------
kubectl get deployment ( we can see 1 deployment object )




kubectl get pods  ( we should get 3 pods )



We can anyways perform scaling, apart from that we can perform rolling updates.

kubectl get all  (  we get all the objects )
Take a note of the full name of the deployment object

 
deployment.apps/nginx-deployment


To perform rolling update
-----------------------------

kubectl --record deployment.apps/nginx-deployment  set image deployment.v1.apps/nginx-deployment nginx=nginx:1.9.1

We get a message ( image updated )

kubectl get pods
To know more about pod
------------------------
kubectl describe pods podname

nginx-deployment-5f8d94b9f7-vcljb




kubectl describe pods nginx-deployment-6bb68879f9-66dmh | less

we can see as Image: nginx:1.9.1


:q
( It will take some time )

kubectl  get pods

++++++++++++++++++++++++++++++++++++++++++++




++++++++++++++++++++++++++++++++++++



Service Object
-----------------------

This is used for network load balancing and port mapping.
Service Object uses 3 ports
1. Target port -  Its is pod or container port 
2. port - Refers to service port.
3. hostPort -  Refers to host machine port to make it accessable from external network.



Service Objects are classified into 3 types

1. clusterIP: This is default type of service object used in kubermetes and it is used when we want the pods in the cluster to communicate with each other and not with external network.


2. nodePort: This is used, if we want to access the pods from an external network and it also performs network load balancing. ie Even if a pod is running on a specific slave, we can access it from other slave in the cluster.


3. LoadBalancer:    This is similar to nodePort. It is used for external connectivity of a pod and also network load balancing and it also assigns a  public ip for all the nodes  combined together.

+++++++++++++++++++++++





vim pod-definition1.yml

We will be creating a service object for the labels used in pod-definition1.yml

kubectl create -f pod-definition1.yml

As we know by pod will be created using the above command.

We want to create service object for the above pod

Ex: Create a service definition file for port mapping on nginx pod


vi service1.yml

---
apiVersion: v1
kind: Service
metadata:
 name: nginx-service
 labels:
  author: sunil
spec:
 type: NodePort
 ports:
  - targetPort: 80
    port: 80
    nodePort: 30008
 selector:
  author: sunil
  type: reverse-proxy
... 

:wq

kubectl create -f service1.yml


Observation: Along with the pod, service object gets created.
This service object is type Nodeport. Hence can be accessed from external network.


gcloud compute firewall-rules create rule3 --allow tcp:30008

vi service1.yml

---
apiVersion: v1
kind: Service
metadata:
 name: nginx-service
 labels:
  author: sunil
spec:
 type: NodePort
 ports:
  - targetPort: 80
    port: 80
    nodePort: 30008
 selector:
  author: sunil
  type: reverse-proxy
... 

:wq

 
kubectl create -f service1.yml

Now, the nginx pod is accessable externally

kubectl get nodes -o wide

As we have created nodePort, we should able to access from any node.

Take external_IP  from anynode

35.193.13.112.30008   ( We should be able to access nginx )

34.122.192.207:30008

10.128.0.16:30008




If service object is not created,  we used to identify in which node the pod is running, take that node IP, from that node IP, we used to access that application.

( Note: We need to open 30008 port in cluster )

++++++++++++++++++++++


Kubernetes Project
---------------
This is a python based application which is used for accepting a vote ( voting app ).
This application accepts the vote and passes it to temporary db created using redis. From redis, the data is passed to worker application created using dotnet. Dotnet based application analyses the data and stores it in permanant database created using postgres.
From postgres database, results can be seen on an application created using node JS.

    
Have a look at the project Architecture.

Redis and postgres pod needs to assigned as cluster IP.
As cluster Ip is used for internal communication.

Voting App and Result App needs to be assigned as loadbalance type.

We need to create 5 definition files.

These 5 images related to this project is available in hub.docker.com
Using those images, we will create pods.
We need to create 5 pod definition files
We need to create 4 service files

We will be creating these definition files using pycharm.


 
vim voting-app-pod.yml


---
apiVersion: v1
kind: Pod
metadata:
  name: voting-app-pod
  labels:
    name: voting-app-pod
    app: demo-voting-app
spec:
  containers:
    - name: voting-app
      image: dockersamples/examplevotingapp_vote
      ports:
        - containerPort: 80
...


:wq


vim result-app-pod.yml

apiVersion: v1
kind: Pod
metadata:
  name: result-app-pod
  labels:
    name: result-app-pod
    app: demo-voting-app
spec:
 containers:
   - name: result-app
     image: dockersamples/examplevotingapp_result
     ports:
       - containerPort: 80
...


:wq



vim worker-app-pod.yml


---
apiVersion: v1
kind: Pod
metadata:
  name: worker-app-pod
  labels:
    name: worker-app-pod
    app: demo-voting-app
spec:
  containers:
   - name: worker-app
     image: dockersamples/examplevotingapp_worker
...


:wq


vim redis-pod.yml

---
apiVersion: v1
kind: Pod
metadata:
  name: redis-pod
  labels:
    name: redis-pod
    app: demo-voting-app
spec:
  containers:
   - name: redis
     image: redis
     ports:
      - containerPort: 6379
...


:wq



vim postgres-pod.yml

---
apiVersion: v1
kind: Pod
metadata:
  name: postgres-pod
  labels:
    name: postgres-pod
    app: demo-voting-app
spec:
  containers:
    - name: postgres
      image: postgres:9.4
      ports:
        - containerPort: 5432
...


We are done with 5 pod definiton files.
We need to create 4 service definiton files.


vim redis-service.yml

---
apiVersion: v1
kind: Service
metadata:
  name: redis-service
  labels:
    name: redis-service
    app: demo-voting-app
spec:
  ports:
    - port: 6379
      targetPort: 6379
  selector:
    name: redis-pod
    app: demo-voting-app


:wq

Note: As we have not specified the type of service object, by default it creates service object to type Cluster_IP



vim   result-app-service.yml

apiVersion: v1
kind: Service
metadata:
  name: result-service
  labels:
    name: result-service
    app: demo-voting-app
spec:
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 80
  selector:
    name: result-app-pod
    app: demo-voting-app



:wq


The above two service objects are of type load balancer. we can access it from the external network.


Open gitbash from the location where all the definition files are saved.

$ git init
$ git add .
$ git commit -m "a"

Open github ---> create new repository

Repository name -  kuber_project

upload the files from local repository to remote repository using the two commands

$ git remote add  XXXXX
$ git push XXXX

We should able to see the definition files in github repository ( Total 9 files )

We need to download the 9 files into kubernetes cluster.


Login to GCP console
Create kubernetes cluster
Connect to the cluster

Get the repository URL in github.

$ git clone rep_url

$ git clone https://github.com/tparshu/kube_project_.git


( Observation all the definition files will be downloaded )

$ cd kuber_project
$ ls   ( we get the files )

$ kubectl create -f  voting-app-pod.yml

$ kubectl  get pods  ( we should get one pod )

$ kubectl create -f  redis-pod.yml

$ kubectl create -f  worker-app-pod.yml

$ kubectl create -f postgres-pod.yml

$  kubectl create -f result-app-pod.yml

Now, we need to run service definition files

$   kubectl create -f voting-app-service.yml

$   kubectl create -f  redis-service.yml

$   kubectl create -f postgres-service.yml

$   kubectl create -f result-app-service.yml

To get all the information

$ kubectl get all

We can see 5 pods and 4 services created.


Observation: worker pod  also failed.

++++++++++++++++++++++++++++

These images are coming from community called dockersamples
Connection between workerpod and postgresPod is creating issues.

Go to service&ingress option in the kuberneted dashboard
We can see the four services, which are created.


Click on endpoint ( IP ) of voting Application
Click in URL, we get Voting App ( CATS / DOGS )  -- This is python based App.

Click on endpoint ( IP ) of result Application

Click in URL, we get Result App
 

++++++++++++++++++++++++++++++++++++++




