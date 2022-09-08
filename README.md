[![License](https://img.shields.io/badge/License-MIT-blue)](#license "Go to license section") [![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2Fsagarkhandve%2Fkubernetes-cluster.git&count_bg=%2308DD09&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=hits&edge_flat=true)](https://hits.seeyoufarm.com)

### Lightweight, easy, fast Kubernetes distribution with a very small footprint.
![kubernetes_logo_icon_168359](https://user-images.githubusercontent.com/90393971/187159759-d19a8782-d9c6-46af-9a57-7ec015f63a15.png)

### Install Master

```
curl -sfL https://get.k3s.io | sh -s - --no-deploy traefik --write-kubeconfig-mode 644 --node-name k3s-master-01
```

### Install Worker

Grab token code from the master node to be able to add worked nodes to it: 

```
cat /var/lib/rancher/k3s/server/node-token
```

Install k3s on the worker node and add it to our cluster:
```
curl -sfL https://get.k3s.io | K3S_NODE_NAME=k3s-worker-01 K3S_URL=https://<IP>:6443 K3S_TOKEN=<TOKEN> sh - 
```
### Install nginx ingress controller


Website: https://kubernetes.github.io/ingress-nginx/
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.2.1/deploy/static/provider/cloud/deploy.yaml
```

#### Important note for AWS, Azure, GCP

I can't explain it in detail but if you run a VM on AWS, Azure or GCP the "ingress-nginx" will just pick up the private IP as external IP. You need to manually edit the service to make your public IP address available for nginx, so it can start listening on your public IP address.
```
kubectl -n ingress-nginx edit svc ingress-nginx-controller
```
Add your IP as list to `spec.externalIPs` like so:

```
  spec:
    externalIPs:
    - <YOUR_IP>
```

### Additional information

You can change the settings of k3s by changing the service settings e.g. with `nano /etc/systemd/system/k3s.service`.

Make sure to restart the service afterwards: `systemctl restart k3s`

In many cases you can just run the installer with different variables again and it will configure your cluster accordingly without deleting it in the first place.

### Deploy demo application
```
kubectl apply -f manifest.yaml
```
