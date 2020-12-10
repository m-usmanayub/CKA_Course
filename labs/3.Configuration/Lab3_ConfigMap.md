1. How can we check the configmaps in the environment

<details><summary>Show</summary>
<p>

```bash
kubectl get configmap
```
</p>
</details>

2. Create a configmap named cm-color with data APP_COLOR=darkblue

<details><summary>Show</summary>
<p>

```bash
kubectl create configmap cm-color --from-literal=APP_COLOR=darkblue
```
</p>
</details>

3. Create the pod using image kodekloud/webapp-color and use the configmap created 

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp-color
  namespace: default
  labels:
    name: webapp-color
spec:
  containers:
  - env:
    - name: APP_COLOR
      value: pink
    image: kodekloud/webapp-color
    imagePullPolicy: Always
    name: webapp-color
```
</p>
</details>

4. Expose the pod using service type nodePort and browse to see the color

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Service
metadata:
  name: webapp-color-service
spec:
  ports:
  - nodePort: 30080
    port: 8080
    protocol: TCP
    targetPort: 8080
  selector:
    name: webapp-color
  sessionAffinity: None
  type: NodePort
```
</p>
</details>
