# Steps

Create k8s cluster 

```sh
$ minikube start -p meetup-demo --kubernetes-version=v1.15.7 --cpus 4 --memory 4096
```
Create Whitelisted namespace where you can able to play

```sh
$ kubectl create ns test-kill-ns
```

Create deployment in `test-kill-ns` along with `kube-monkey` labels injected

```sh
$ kubectl create -f nginx-deployment.yaml
$ kubectl expose deployment nginx-deployment --type=NodePort --name=svc-kill-ns -n test-kill-ns
```
Create `kube-monkey` deployments in kube-system

```sh
$ kubectl create -f configmap.yaml 
$ kubectl create -f deployment.yaml
```

Let's verfiy does `kube-monkey` started terminiating pods from victim deployments ?

```sh
kubectl logs -f deployment.apps/kube-monkey --namespace=kube-system
```




