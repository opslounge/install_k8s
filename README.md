# Kubernetes ansible deployment

This document details how to use the SG demo lab to build a Kubernetes (K8's) environment for demo.


## Dependancies

you will need the following to begin

- SSH into ansible jump server 


## Outcome

This demo will build a 3 node K8's cluster from scratch using ansible to 
deploy Virtual Machines, then to configure them, and lastly to install a K8's cluster.

you can then follow the PSO install instructions listed here:



## Build the Virtual Machines creation playbook

Log into the ansible server using provided credentials. 

browse to the kcluster dir

```
cd kcluster/
```

Build VM's using the clonevms.yaml playbook

```
ansible-playbook clonevms.yaml
```

### Prep Virtual Machines for K8's

Execute the kubeprep playbook to set them up for K8's

```
ansible-playbook kubeprep.yaml
```


### Install K8's cluster

Execute the setup_master_node playbook to build configure 
the master node and configure K8's

```
ansible-playbook setup_master_node.yml
```


### Setup worker nodes

Execute the setup_worker_nodes playbook to join worker nodes to the cluster

```
ansible-playbook setup_worker_nodes.yml
```


### Post cluster operations

Currently there is a bug with firwalls not quite sorted out. Please re run the 
kubeprep playbook to disable firewalls post setup. 

``` 
ansible-playook kubeprep.yaml
```


### Install and setup PSO

At this point the cluster is now up and running. 

ssh as root to the master node.  You will be able to execute K8's commands on the cluster. 

You can use these instructions to install PSO on the cluster. 

[PSO install](https://github.com/opslounge/install_pso)


### Tear down of environment

You can tear down this environment after your finished using by executing the del playbook

```
ansible-playbook del.yaml
```

NOTE: future enhancements will include a weekly teardown of this environment manually. 



* **Andy Parsons** - - [opslounge](https://github.com/opslounge)



