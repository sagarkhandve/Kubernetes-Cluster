[![License](https://img.shields.io/badge/License-MIT-blue)](#license "Go to license section")

### Kubernetes cluster in 'Ubuntu' or any 'Debian' based distros.
![kubernetes_logo_icon_168359](https://user-images.githubusercontent.com/90393971/187159759-d19a8782-d9c6-46af-9a57-7ec015f63a15.png)


### ssh into Master-Node as `root`user and run the given command.
```
curl -sfL https://get.k3s.io | sh -s - --no-deploy traefik --write-kubeconfig-mode 644 --node-name `k3s-master-node`

### Grab token from the master node to be able to add worked nodes to it:
cat /var/lib/rancher/k3s/server/node-token

### ssh into Worker-Node as `root` user and run the given command by updating `Worker-Node` name, IP of the `Master-Node` and the `Token Key' which we grabbed from the Master-Node.
curl -sfL https://get.k3s.io | K3S_NODE_NAME=Worker-Node-01 K3S_URL=https://<IP>:6443 K3S_TOKEN=<TOKEN> sh - 
```



