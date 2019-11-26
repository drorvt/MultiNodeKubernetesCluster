<!-- ABOUT THE PROJECT -->

setup multi-node kubernetes cluster with Vagrant and Ansible

### Architecture:
We will setup a nodes Kubernetes cluster on Ubuntu 18.04
### Prerequisites
We need to install :

- [Kubernetes 1.14+](https://github.com/kubernetes/kubernetes/)
- [Ansible 2.0+](https://github.com/ansible/ansible/)
- [Vagrant 2.2+](https://github.com/hashicorp/vagrant/)
- [Virtualbox 6.0+](https://www.virtualbox.org/wiki/Downloads)

### Installation Application
1. roles : Roles provide a framework for fully independent, or interdependent collections of variables, tasks, files, templates, and modules.

### example from project :

- [calico](https://docs.projectcalico.org/v3.10/introduction/)
- [docker]
- [helm](https://helm.sh/)
- [join](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-join/)
- [kubeadm,kubelet,kubectl](https://kubernetes.io/docs/tasks/tools/)


2. playbook:  Ansible playbooks, executing the defined tasks on the targeted hosts.
 
 hosts: masters
 
    - components
    - docker
    - swap
    - cluster
    - kubelet
    - kubeadm
    - kubeconfig
    - iptables
    - calico
    - token

hosts: nodes

    - components
    - docker
    - swap
    - cluster
    - kubelet
    - iptables
    - join
3.

### How to install and run:

1. Clone this github repo
2. Navigate to k8s-vagrant directory 
```
cd kubernetes.resources/k8s-vagrant/
vagrant up
```
3. ssh into the k8s-master by running the following command:
```
vagrant ssh k8s-master
```
4. You can verify the cluster by checking the nodes. Run the following command to list all the connected nodes:
```
vagrant@k8s-master:~$ kubectl get nodes -o wide
```
5.Check everything worked:
```
vagrant@k8s-master:~$ kubectl get pods -n kube-system
```
6. Deployment SonarQube,Nexus,Jenkinsto Kubernetes with Helm:
```
helm install --name jenkins -f jenkinsValues.yaml stable/jenkins
helm install --name nexus -f nexusValues.yaml sonatype-nexus
helm install --name SonarQube -f SonarQubeValue.yaml stable/sonarqube
```
7. Jenkins pipeline that using maven to compile git, running SonarQube test and upload war to nexus, create docker image and upload it to nexus registry




