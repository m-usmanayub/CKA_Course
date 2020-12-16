## Lab 6 : Multi-Container Pods

1.  Create a namespace cka-lab19.
    
  
  <details><summary>Show</summary>

<p>

```bash
kubectl create ns cka-lab19

```

</p>
</details>

  

2.  Create a pod in the namespace using which has the following containers using their respective images.
    
Pod Name: multi-container-pod

Image1: nginx:alpine

name: nginx

Image2: redis:alpine

name: redis

Image3: consul

name: consul

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata: 
  name: multi-container-pod
  namespace: cka-lab19
spec:
  containers: 
  - image: nginx:alpine
    name: nginx
  - name: redis
    image: redis:alpine
  - image: consul
    name: consul

```

</p>
</details>  

3.  Delete the namespace

<details><summary>Show</summary>
<p>

```bash

kubectl delete ns cka-lab19

```

</p>
</details>
