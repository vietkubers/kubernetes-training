Set up a single cluster with minikube behind proxy
==================================================

Preparing environment
=====================
OS: Ubuntu 16.04 LTS

Clear previous installation if you've already done it before:
```sh
$ sudo kubeadm reset
$ sudo rm -rf /var/lib/minikube/certs/
$ sudo rm -rf /etc/kubernetes/
$ sudo rm -rf /etc/lib/etcd/
$ sudo rm -rf /.kube
$ sudo rm -rf /.minikube
```

Config apt proxy:
```sh
$ sudo vim /etc/apt/apt.conf
...
Acquire::http::proxy "http://[Proxy_Server]:[Proxy_Port]/";
Acquire::HTTP::proxy "http://[Proxy_Server]:[Proxy_Port]/";
```

Please note that some distros do not keep proxy settings
Make sure "sudo" keeps these settings including: http_proxy, https_proxy & no_proxy
```sh
$ sudo visudo
#Add the following line
Defaults env_keep += "ftp_proxy http_proxy https_proxy no_proxy"
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
```

Deploy single cluster with minikube --vm-driver none
```sh
$ export no_proxy=$no_proxy,[Your_Ip]
$ export CHANGE_MINIKUBE_NONE_USER=true
$ sudo minikube start --vm-driver=none --logtostderr
```
Run minikube without sudo
```sh
$ vi .kube/config
- cluster:
    certificate-authority: /home/kuber/.minikube/ca.crt
    server: https://10.0.2.15:8443
  name: minikube
...
user:
    client-certificate: /home/kuber/.minikube/client.crt
    client-key: /home/kuber/.minikube/client.key
```


Happy hacking!
==============
