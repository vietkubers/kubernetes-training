Set up a single cluster with minikube behind proxy
==================================================

Preparing environment
=====================
OS: Ubuntu 16.04 LTS

Clear previous install if you've already done it before:
```sh
$ sudo kubeadm reset
$ sudo rm -rf /var/lib/minikube/certs/
$ sudo rm -rf /etc/kubernetes/
$ sudo rm -rf /etc/lib/etcd/
```

Config apt proxy:
```sh
$ sudo vim /etc/apt/apt.conf
...
Acquire::http::proxy "http://[Proxy_Server]:[Proxy_Port]/";
Acquire::HTTP::proxy "http://[Proxy_Server]:[Proxy_Port]/";
```

Set up kubernetes repo:
```sh
$ sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
$ cat <<EOF > kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF
$ sudo mv kubernetes.list /etc/apt/sources.list.d/kubernetes.list
$ sudo apt-get update
```

Config proxy for docker:
```sh
$ sudo mkdir -p /etc/systemd/system/docker.service.d
$ sudo vim /etc/systemd/system/docker.service.d/http-proxy.conf

[Service]
Environment="HTTP_PROXY=http://[Proxy_Server]:[Proxy_Port]/"
```
Install minikube:
```sh
$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && sudo install minikube-linux-amd64 /usr/local/bin/minikube
$ sudo apt-get install -y apt-transport-https
$ sudo apt-get install -y docker.io
$ sudo apt-get install -y kubelet kubeadm 
```

Deploy single cluster with minikube --vm-driver none
```sh
$ export no_proxy=$no_proxy,[Your_Ip]
```
Please note that switch to root user, because some distro doesn't keep proxy setting, then:
```sh
# minikube start --vm-driver=none --logtostderr
```

Logout root user and rub:

```sh
$ sudo cp -R /root/.kube $HOME/.kube
$ sudo chown -R $USER $HOME/.kube
$ sudo chgrp -R $USER $HOME/.kube
$ sudo cp -R /root/.minikube $HOME/.minikube
$ sudo chown -R $USER $HOME/.minikube
$ sudo chgrp -R $USER $HOME/.minikube
```

Happy hacking!
==============
