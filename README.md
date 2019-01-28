# kubernetes-training
Summary the training material from LXC to Docker and Kubernetes.  
All the technical articles of [VietKubers](https://vietkubers.github.io/) are located in: https://github.com/vietkubers/vietkubers.github.io/tree/master/pages/mydoc

## LXC
 - namespace:
    - [Network](http://abregman.com/2016/09/29/linux-network-namespace/)
      - [Introduction to Linux Network Namespace](https://www.youtube.com/watch?v=_WgUwUf1d34)
    - [cgroups](/LXC/cgroups.md)
 - seccomp
 - [chroot](/LXC/chroot.md)
 
## Docker

 - Docker lab
   - [Deploying flask app with Dockerfile](/Docker/docker-lab/flask-app)
   - [Docker compose to run Django app](/Docker/docker-lab/django-app)
   - [GUI with Docker](/Docker/docker-lab/firefox-gui)

 - Useful Resources
   - [Awesome-docker](https://github.com/veggiemonk/awesome-docker)
   - [Docker tutorials and labs](https://github.com/docker/labs)

## Kubernetes
  - [Deploying multiple nodes with Kubeadm](/Kubernetes/deploy_multiple_node.md)
  - [Set up a single cluster with minikube behind proxy](/Kubernetes/single_node_minikube_behind_proxy.md)

## Go language

## eBPF and XDP for network
- bcc
- Cilium, Istio, Envoy

## How to contribute to kubernetes community
- [Install minikube](/Kubernetes/single_node_minikube_behind_proxy.md)
- Join Kubernetes slack
- [Github workflow](/contributing_guide/github_workflow.md)

## References
  - https://www.slideshare.net/imesh/an-introduction-to-kubernetes
  - https://medium.com/@ApsOps/an-illustrated-guide-to-kubernetes-networking-part-1-d1ede3322727
  
# License
Copyright © 2018, [VietKubers](https://www.facebook.com/groups/VietKubers/). Released under the [MIT License](https://github.com/vietkubers/kubernetes-training/blob/master/LICENSE).
