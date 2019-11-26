setup multi-node kubernetes cluster with Vagrant and Ansible

Architecture:
We will setup a nodes Kubernetes cluster on Ubuntu 18.04

Prerequisite:

Kubernetes 1.14+
Ansible 2.0+
Vagrant 2.2+
Virtualbox 6.0+

How to install and run:

1. Clone this github repo
2. Navigate to k8s-vagrant directory 
cd kubernetes.resources/k8s-vagrant/
vagrant up

3. ssh into the k8s-master by running the following command:
vagrant ssh k8s-master

4. You can verify the cluster by checking the nodes. Run the following command to list all the connected nodes:
vagrant@k8s-master:~$ kubectl get nodes -o wide

5.Check everything worked:
vagrant@k8s-master:~$ kubectl get pods -n kube-system

6. Deployment to Kubernetes with Helm:
Let's deploy a on Kubernetes cluster using Helm. Helm is a package manager for Kubernetes that allows developers deploy applications on Kubernetes clusters.
