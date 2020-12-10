1. Deploy a pod named nginx-pod using the nginx:alpine image.
<details><summary>Show</summary>
<p>

```bash
kubectl run nginx-pod --image=nginx:alpine
```

</p>
</details>

2. Deploy a redis pod using the redis:alpine image with the labels set to tier=db.
<details><summary>Show</summary>
<p>

```bash
kubectl run redis --image=redis:alpine -l tier=db
```

</p>
</details>

3. Create a service redis-service to expose the redis application within the cluster on port 6379.
<details><summary>Show</summary>
<p>

```bash
kubectl expose pod redis --port=6379 --name redis-service
```

</p>
</details>

4. Create a deployment named webapp using the image kodekloud/webapp-color with 3 replicas
<details><summary>Show</summary>
<p>

```bash
kubectl create deployment webapp --image=kodekloud/webapp-color
```

Then scale the webapp to 3 using command 

```bash
kubectl scale deployment/webapp --replicas=3
```

</p>
</details>

5. Create a new pod called custom-nginx using the nginx image and expose it on container port 8080
<details><summary>Show</summary>
<p>

```bash
kubectl run custom-nginx --image=nginx --port=8080
```

</p>
</details>

6. Create a new namespace called dev-ns.
<details><summary>Show</summary>
<p>

```bash
kubectl create ns dev-ns
```

</p>
</details>

7. Create a new deployment called redis-deploy in the dev-ns namespace with the redis image. It should have 2 replicas.
<details><summary>Show</summary>
<p>
Step 1: Create the deployment YAML file

```bash
kubectl create deployment redis-deploy --image redis --namespace=dev-ns --dry-run=client -o yaml > deploy.yaml
```

Step 2: Edit the YAML file and add update the replicas to 2
Step 3: Run kubectl apply -f deploy.yaml to create the deployment in the dev-ns namespace.
You can also use kubectl scale deployment or kubectl edit deployment to change the number of replicas once the object has been created.

</p>
</details>

8. Create a pod called httpd using the image httpd:alpine in the default namespace. Next, create a service of type ClusterIP by the same name (httpd). The target port for the service should be 80.
Try to do this with as few steps as possible.
<details><summary>Show</summary>
<p>

```bash
kubectl run httpd --image=httpd:alpine --port=80 --expose
```

</p>
</details>
