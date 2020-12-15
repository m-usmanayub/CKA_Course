## Lab 2 : nodeName and nodeSelector

1.  Create a namespace cka-lab15.

<details><summary>Show</summary>
<p>

```bash
kubectl create ns cka-lab15
```

</p>
</details>
    

  

2.  Create a pod using image httpd in the namespace which must be manually scheduled on worker node using nodeName property.
  
<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: httpd
spec:
  containers:
  - name: httpd
    image: httpd
  nodeName: <>

```

</p>
</details>

  

3.  Label the worker node with size=large
    

  <details><summary>Show</summary>
<p>

```bash
kubectl label node <> size=large

```

</p>
</details>

4.  Create a pod using nginx image in the lab namespace using nodeSelector property of the podSpec having the value size=large
    

  <details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    env: test
spec:
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
  nodeSelector:
    size: large
```

</p>
</details>

5.  Delete the namespace cka-lab8 after completing the lab.



<details><summary>Show</summary>
<p>

```bash
kubectl delete ns cka-lab8
```

</p>
</details>
