## Practice Questions - Scaling

1.  Create a deployment with image nginx:1.18.0, called nginx-deploy, having 2 replicas, defining port 80 as the port.
    

  <details><summary>Show</summary>
<p>

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    name: nginx
  name: nginx-deploy
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx-deploy
  template:
    metadata:
      labels:
        app: nginx-deploy
    spec:
      containers:
      - image: nginx:1.18.0
        name: nginx
        ports: 
        - containerPort: 80
```

</p>
</details>

2.  Extract the YAML of the deployment
    

  <details><summary>Show</summary>
<p>

```bash
kubectl get deploy nginx-deploy -o yaml
```

</p>
</details>

3.  Check the rollout status of the deployment
    

  <details><summary>Show</summary>
<p>

```bash
kubectl rollout status deploy nginx-deploy
```

</p>
</details>

4.  Update the deployment to nginx:1.19
    
<details><summary>Show</summary>
<p>

```bash
kubectl set image deploy nginx-deploy nginx=nginx:1.19
```

</p>
</details>
  

5.  Check the rollout history and confirm
    
<details><summary>Show</summary>
<p>

```bash
kubectl rollout history deploy nginx-deploy
```

</p>
</details>
  

6.  Rollback the deployment to image 1.18.0
    

 <details><summary>Show</summary>
<p>

```bash
kubectl rollout undo deploy nginx-deploy
```

</p>
</details> 

7.  Update the deployment to nginx:cka
    

  <details><summary>Show</summary>
<p>

```bash
kubectl set image deploy nginx-deploy nginx=nginx:cka
```

</p>
</details>

8.  Check the status and rollout history.
    
<details><summary>Show</summary>
<p>

```bash
kubectl rollout status deploy nginx-deploy
kubectl rollout history deploy nginx-deploy
```

</p>
</details>
  

9.  Revert to nginx:1.19 using rollout command.
    

  <details><summary>Show</summary>
<p>

```bash
kubectl rollout undo deploy nginx-deploy --to-revision=
kubectl describe deploy nginx-deploy | grep Image:
kubectl rollout status deploy nginx-deploy```
```

</p>
</details>
  

11.  Delete the Deployment

<details><summary>Show</summary>
<p>

```bash
kubectl delete deploy nginx-deploy
```

</p>
</details>
