## Lab 7 : Updating Deployments

1.  Create a namespace cka-lab20
    
<details><summary>Show</summary>
<p>

```bash
kubectl create ns cka-lab20
```

</p>
</details>
  

2.  Create a deployment named nginx-deploy in the namespace using nginx image version 1.17 with three replicas and container port 80. Check that the deployment rolled out and show running pods.
    
<details><summary>Show</summary>
<p>

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    name: nginx
  name: nginx-deploy
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-deploy
  strategy: {}
  template:
    metadata:
      labels:
        app: nginx-deploy
    spec:
      containers:
      - image: nginx:1.17
        name: nginx
        ports: 
        - containerPort: 80

```

</p>
</details>
  

3.  Expose the deployment using nodePort service and check by browsing the URL.
    
<details><summary>Show</summary>
<p>

```bash
kubectl expose deployment nginx-deploy --port=80 --target-port=80 

then edit the service and change the type to NodePort 
```

</p>
</details>
  

4.  Scale the deployment to 5 replicas and check the status again. Then change the image tag of nginx container from 1.17 to 1.19.
    

  <details><summary>Show</summary>
<p>

```bash
kubectl scale deployment nginx-deploy --replicas=5

kubectl rollout status deployment nginx-deploy

kubectl get deploy

kubectl get pods

kubectl set image deploy/nginx-deploy nginx=nginx:1.19
```

</p>
</details>

5.  Check the history of the deployment and rollback to previous revision. Then check that the nginx image was reverted to 1.17.



<details><summary>Show</summary>
<p>

```bash
kubectl rollout history deployment nginx-deploy
kubectl rollout undo deployment nginx-deploy
```

</p>
</details>
