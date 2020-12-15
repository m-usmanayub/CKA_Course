## Lab 3 : Node Affinity

1.  What are the values set to the label beta.kubernetes.io/arch and beta.kubernetes.io/os .
    

<details> <summary> Show </summary>

<p>

```bash
kubectl get nodes --show-labels 
or 
kubectl describe node <nodename>

```

</p>
</details>

  

2.  Apply a label disk=ssd to a worker01 node.
    
<details><summary>Show</summary>
<p>

```bash
kubectl label node worker01 disk=ssd
```

</p>
</details>
  

3.  Create a new deployment named redis-prod with the redis image and 2 replicas.
    

  <details><summary>Show</summary>
<p>

```bash
kubectl create deployment redis-prod --image=redis
kubectl scale deployment redis-prod --replicas=2
```

</p>
</details>

4.  Where are the pods of the deployment placed on?
    

  <details><summary>Show</summary>
<p>

```bash
kubectl get pods -o wide
on master and worker nodes
```

</p>
</details>

5.  Set Node Affinity to the deployment to place the pods on worker01 using label assigned above.
    

  <details><summary>Show</summary>
<p>

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-prod
spec:
  replicas: 2
  selector:
    matchLabels:
      run: redis
  template:
    metadata:
      labels:
        run: redis
    spec:
      containers:
      - image: redis
        imagePullPolicy: Always
        name: redis
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: disk
                operator: In
                values:
                - ssd
```

</p>
</details>

6.  Check if the pods are placed on worker01 only.
    
<details><summary>Show</summary>
<p>

```bash
kubectl get pods -o wide 
```

</p>
</details>
  

7.  Create a new deployment named nginx-prod with the nginx image and 2 replicas, and ensure it gets placed on the master/controlplane node only.Use the label - node-role.kubernetes.io/master - set on the master/controlplane node.

<details><summary>Show</summary>
<p>

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-prod
spec:
  replicas: 2
  selector:
    matchLabels:
      run: nginx
  template:
    metadata:
      labels:
        run: nginx
    spec:
      containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: node-role.kubernetes.io/master
                operator: Exists

```

</p>
</details>
