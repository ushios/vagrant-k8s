# vagrant-k8s
runnnig k8s on vm

# Running kubernetes

Run all vm
```console
$ vagrant up
```

Init kubeadm and get init token
```console
$ vagrant ssh master01
master01 $ sudo kubeadm init

...

as root:
  kubeadm join --token <token> <master-ip>:<master-port>
```

Create configuration
```console
mastesr01 $ mkdir -p $HOME/.kube
mastesr01 $ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
mastesr01 $ sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Create flannel pods
```console
master01 $ sudo su -
masetr01 $ kubectl apply -f https://git.io/weave-kube
```

Add mster02 to kubernetes cluster
```console
$ vagrant ssh master02
master02 $ sudo su -
master02 $ kubeadm join --token <token> 192.168.100.10:<master-port>
```
