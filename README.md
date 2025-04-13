# k8s-learning-handson

This is to learn kubernetes and take notes of learnings

# Diagram

<img width="355" alt="image" src="https://github.com/user-attachments/assets/7e9cdea9-6254-4cbe-a0f8-4c51671b997e" />

# K3S cluster alternative to k8s setup

---

> [!NOTE]
>
> As this setup is only for learning purpose of kubernetes, we are

1. Create VPC - in AWS account with 3 Avl Zones and let's go with public subnets only :
   1. Edit inbound rules for Security group in that VPC
1. Create Launch Template for EC2 instance to launch 3 similar instances in 3 avl zone
1. Config : 1 Master node , 2 Worker node
1. K3S installation follow documentation and Some help from ChatGPT

> [!NOTE]
>
> ## Master node:

```sh
sudo su
hostnamectl set-hostname master-n1
curl -Lo /usr/local/bin/k3s https://github.com/k3s-io/k3s/releases/download/v1.26.5+k3s1/k3s; chmod a+x /usr/local/bin/k3s
nohup k3s server --write-kubeconfig-mode 644 &
sudo ln -s /usr/local/bin/k3s /usr/local/bin/kubectl
echo "nohup k3s server --write-kubeconfig-mode 644 &" > startk3s_cluster.sh
echo "sudo pkill -f k3s" > stopk3s_cluster.sh
```

### Token Generate

```sh
cat /var/lib/rancher/k3s/server/node-token
```

> [!NOTE]
>
> ## Worker nodes:

```sh
sudo su
hostnamectl set-hostname worker-n1
curl -Lo /usr/local/bin/k3s https://github.com/k3s-io/k3s/releases/download/v1.26.5+k3s1/k3s; chmod a+x /usr/local/bin/k3s
```

### Join the cluster

```sh
nohup k3s agent --server https://@MASTER_NODE_PRIVATE_IP@:6443 --token @TOKEN@ &
```

> `nohup k3s agent --server https://10.0.45.219:6443 --token K10e613e4fd147382af26fc6a85c193fd8fad66ec26900a5cf3e4b129c065e48309::server:fc8f69f0608c27abb8322611b972dc79 &`

## O/P from master node after worker node joins:

```bash

[root@ip-10-0-14-179 ec2-user]# kubectl get nodes
NAME        STATUS   ROLES                  AGE   VERSION
master-n1   Ready    control-plane,master   14m   v1.26.5+k3s1
worker-n1   Ready    <none>                 18m   v1.26.5+k3s1
```

# 1 Pod Deployment :

```bash
[root@ip-10-0-14-179 ec2-user]# vi deployPod.yml
[root@ip-10-0-14-179 ec2-user]# cat deployPod.yml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80

[root@ip-10-0-14-179 ec2-user]# kubectl apply -f deployPod.yml
pod/nginx-pod created
[root@ip-10-0-14-179 ec2-user]# kubectl get pods
NAME        READY   STATUS              RESTARTS   AGE
nginx-pod   0/1     ContainerCreating   0          5s
[root@ip-10-0-14-179 ec2-user]#
[root@ip-10-0-14-179 ec2-user]# kubectl get pods
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          10s
```

# Check which node Pod is Running :

```bash
[root@ip-10-0-14-179 ec2-user]# kubectl get pod nginx-pod -o wide
NAME        READY   STATUS    RESTARTS   AGE   IP          NODE        NOMINATED NODE   READINESS GATES
nginx-pod   1/1     Running   0          50s   10.42.2.4   worker-n1   <none>           <none>
```

## ✅ How to Use `k3s` / `kubectl` as a Normal User (AWS Linux 2023)

To use `k3s` and `kubectl` from a **non-root (normal) user**, follow these steps:

---

### ✅ 1. Add `kubectl` to User's `PATH`

By default, `k3s` installs `kubectl` as a symlink. Create the symlink manually:

```bash
sudo ln -s /usr/local/bin/k3s /usr/local/bin/kubectl
```

```sh
mkdir -p ~/.kube
sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
sudo chown $(id -u):$(id -g) ~/.kube/config
```

> Replace 127.0.0.1 with your master node's IP address:

```sh
sed -i 's/127.0.0.1/<your-master-ip>/' ~/.kube/config
```
