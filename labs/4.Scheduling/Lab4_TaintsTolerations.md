## Lab 4 : Taints and Tolerations

1.  Check the taints on master and worker nodes
    
<details><summary>Show</summary>
<p>

```bash
kubectl get nodes -o yaml or kubectl describe node <nodename>
```

</p>
</details>
  

2.  Create a taint on worker01 with key of ''size”, value of ‘medium’' and effect of 'NoSchedule'
    
<details><summary>Show</summary>
<p>

```bash
kubectl taint nodes <enter worker node name here> size=medium:NoSchedule
```

</p>
</details>
  

3.  Create an nginx pod with the name of nginx-med
    
<details><summary>Show</summary>
<p>

```bash
kubectl run nginx-med --image=nginx
```

</p>
</details>
  

4.  Is the pod running? Check the status and find the reason
    
<details><summary>Show</summary>
<p>

```bash
The pod is in pending state
```

</p>
</details>
  

5.  How can we make the pod to run? Create another pod with correct definition using image redis and toleration to run on worker node
    
<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: redis
spec:
  containers:
  - image: redis
    name: redis
  tolerations:
  - key: size
    value: medium
    effect: NoSchedule
    operator: Equal
```

</p>
</details>
  

6.  Remove the taint of the master node
    
<details><summary>Show</summary>
<p>

```bash

```

</p>
</details>
  

7.  Check the first pod must be running now on master
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

8.  Remove the taint of the worker node and add the taint of the master node back

<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
