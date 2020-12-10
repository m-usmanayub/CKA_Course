## Lab 6 - Services


1. Create all the resources in the cka-lab6 ns and delete the ns after completion.

  <details><summary>Show</summary>
<p>

```bash
kubectl create ns cka-lab6

```
</p>
</details>

2. How many Services exist on the system?
  <details><summary>Show</summary>
<p>

```bash
kubectl get services
```
</p>
</details>

3. Check the Default kubernetes service and find out its service type
  <details><summary>Show</summary>
<p>

```bash
ClusterIP
```
    
</p>
</details>

4.  Identify the target port of the default kubernetes service

  <details><summary>Show</summary>
<p>

```bash
6443
```
</p>
</details>

5. Identify the labels on the default kubernetes service
  <details><summary>Show</summary>
<p>

```bash
k describe svc kubernetes
```
</p>
</details>

6. How many Endpoints are attached on the 'kubernetes' service?
  <details><summary>Show</summary>
<p>

```bash
kubectl get endpoints kubernetes
or 
k describe svc kubernetes
```
</p>
</details>

7. Create a deployment webapp-deploy using image kodekloud/simple-webapp:red having 3 replicas
  <details><summary>Show</summary>
<p>

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: simple-webapp-deployment
  namespace: cka-lab6
spec:
  replicas: 3
  selector:
    matchLabels:
      name: simple-webapp
  template:
    metadata:
      labels:
        name: simple-webapp
    spec:
      containers:
      - image: kodekloud/simple-webapp:red
        imagePullPolicy: IfNotPresent
        name: simple-webapp
        ports:
        - containerPort: 8080
          protocol: TCP

```
</p>
</details>

8.  Create a service using the following parameters
    Name: webapp-service; Type: NodePort; targetPort: 8080; port: 8080; nodePort: 30080; selector: simple-webapp
  <details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Service
metadata:
  name: webapp-service
  namespace: default
spec:
  ports:
  - nodePort: 30080
    port: 8080
    protocol: TCP
    targetPort: 8080
  selector:
    name: simple-webapp
  type: NodePort
```
</p>
</details>

9. Try to access the deployment using Node IP and port 30080  
  <details><summary>Show</summary>
<p>

```bash
192.168.99.141:30080
```
</p>
</details>

