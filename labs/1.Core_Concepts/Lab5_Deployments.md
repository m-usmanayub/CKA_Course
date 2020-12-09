## Lab 5 - Deployments


1. Create a namespace cka-lab5

  <details><summary>Show</summary>
<p>

```bash
kubectl create ns cka-lab5
```
</p>
</details>

2. Create a file called deploy.yaml that declares a deployment with name nginx-deploy in the cka-lab5 namespace, with three replicas running the nginx:1.16 image. Each pod should have the label app=revproxy. The deployment should also have the label client=user.
  <details><summary>Show</summary>
<p>

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    client: user
  name: nginx-deploy
spec:
  replicas: 3
  selector:
    matchLabels:
      app: revproxy
  strategy: {}
  template:
    metadata:
      labels:
        app: revproxy
    spec:
      containers:
      - image: nginx:1.16
        name: nginx
```
                     kubectl apply -f deploy1.yaml -n cka-lab5

</p>
</details>

3.  Create a new Deployment in the cka-lab5 namespace with the below attributes using your own deployment definition file:
    Name: httpd-fe; Replicas: 3; Image: httpd:2.4-alpine

  <details><summary>Show</summary>
<p>

```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: httpd-fe
  name: httpd-fe
spec:
  replicas: 3
  selector:
    matchLabels:
      app: httpd-fe
  strategy: {}
  template:
    metadata:
      labels:
        app: httpd-fe
    spec:
      containers:
      - image: httpd:2.4-alpine
        name: httpd
```
       kubectl apply -f deploy2.yaml --namespace=cka-lab5      
</p>
</details>

4. Delete the namespace created in the first step

  <details><summary>Show</summary>
<p>

```bash
kubectl delete ns cka-lab5
```
</p>
</details>
