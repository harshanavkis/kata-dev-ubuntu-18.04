# Possible problems while developing for Kata Containers in ubuntu 18.04

- [ ] Step 6: And deploy k8s with the new "kata" runtimeclass, requires the following changes
```diff
diff --git a/.ci/install_kubernetes.sh b/.ci/install_kubernetes.sh
index 77f1ddcd..86631099 100755
--- a/.ci/install_kubernetes.sh
+++ b/.ci/install_kubernetes.sh
@@ -34,7 +34,7 @@ EOF"
        chronic sudo -E apt install --allow-downgrades -y kubelet="$kubernetes_version" kubeadm="$kubernetes_version" kubectl="$kubernetes_version"
 elif [ "$ID" == "centos" ] || [ "$ID" == "fedora" ]; then
        if [ "$(command -v kubelet)" != "" ]; then
-               yum autoremove kubelet -y
+               sudo yum autoremove kubelet -y
        fi
        url="https://packages.cloud.google.com/yum/repos/kubernetes-el7-${ARCH}"
        echo "Install ${url} for ${ARCH}"
```


- [ ] Step 8: Check everything was deployed
```sh
$ kubectl get pods -A

NAMESPACE     NAME                                READY   STATUS    RESTARTS   AGE
kube-system   coredns-558bd4d5db-9zstz            0/1     Running   0          23m
kube-system   coredns-558bd4d5db-vg6pg            0/1     Running   0          23m
kube-system   etcd-localhost                      1/1     Running   0          23m
kube-system   kube-apiserver-localhost            1/1     Running   0          23m
kube-system   kube-controller-manager-localhost   1/1     Running   0          23m
kube-system   kube-flannel-ds-kljm7               1/1     Running   0          23m
kube-system   kube-proxy-c7s2n                    1/1     Running   0          23m
kube-system   kube-scheduler-localhost            1/1     Running   0          23m

```

```sh
$ kubectl get runtimeClass

No resources found

```
