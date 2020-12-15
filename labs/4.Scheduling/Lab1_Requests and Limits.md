## Lab 1 :Requests and Limits




1- Create a pod redis with a cpu request of 0.5 and limit or 1.

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: redis
  name: redis
spec:
  containers:
  - image: redis
    name: redis
    resources:
      limits:
        cpu: "1"
      requests:
        cpu: 500m
```

</p>
</details>

  

2- Create a pod using the Lab Definition file.

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: memtest
  namespace: default
spec:
  containers:
  - args:
    - --vm
    - "1"
    - --vm-bytes
    - 15M
    - --vm-hang
    - "1"
    command:
    - stress
    image: polinux/stress
    imagePullPolicy: Always
    name: mem-stress
    resources:
      limits:
        memory: 10Mi
      requests:
        memory: 5Mi

```

</p>
</details>


  

3- Check the pod status
<details><summary>Show</summary>
<p>

```
Pod is not running
```

</p>
</details>


  

4- The status 'OOMKilled' indicates that the pod ran out of memory. Identify the memory limit set on the Pod.

<details><summary>Show</summary>
<p>

```


```

</p>
</details>


  

5- Delete the pod and recreate with memory limit of 20M

<details><summary>Show</summary>
<p>

```bash
kubectl delete pods <>

Change the memory limit in the definition file to 20Mi

```

</p>
</details>

  

6- Delete both the pods.

<details><summary>Show</summary>
<p>

```bash
kubectl delete pods 
```

</p>
</details>



  

7- Create an nginx pod using image nginx:1.19.5-alpine with cpu request of 0.5 and memory request of 100m.

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx:1.19.5-alpine
    name: nginx
    resources:
      requests:
        cpu: 500m
        memory: 100Mi
```

</p>
</details>
