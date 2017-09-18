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
(master01) $ sudo kubeadm init --apiserver-advertise-address 192.168.100.10

...

as root:
  kubeadm join --token <token> <master-ip>:<master-port>
```

Create configuration
```console
(master01) $ mkdir -p $HOME/.kube
(master01) $ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
(master01) $ sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Using calico
```console
(master01) $ kubectl apply -f http://docs.projectcalico.org/v2.3/getting-started/kubernetes/installation/hosted/kubeadm/1.6/calico.yaml
```

Add worker01 to kubernetes cluster
```console
$ vagrant ssh worker01
(worker01) $ sudo kubeadm join --token <token> <master-ip>:<master-port>
```

Check nodes
```console
(master01) $ kubectl get nodes
NAME       STATUS    AGE       VERSION
master01   Ready     12m       v1.7.5
worker01   Ready     1m        v1.7.5
```

# References
* [Installing Kubernetes on Linux with kubeadm](http://blog.pichuang.com.tw/Installing-Kubernetes-on-Linux-with-kubeadm/)
* [VirtualBox上でkubeadmを使用してnodeを追加するとエラーが発生する@Qiita](http://qiita.com/smiyaguchi/items/b00705c29884f4c1dcd4)
* [Kubernetes: クラスタ構築が簡単になるkubeadm@Qiita](http://qiita.com/tkusumi/items/5908c91807107551e796)
