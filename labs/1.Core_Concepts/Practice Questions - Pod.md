## Lab 1 - Practice Questions - Pod


1.   How many pods exists in the system
      
      a. In kube-system namespace
     

<details><summary>Show</summary>
<p>

```bash
kubectl get pods -n kube-system 
```

</p>
</details>

 b. In all namespaces

<details><summary>Show</summary>
<p>

```bash
kubectl get pods --all-namespaces
or 
kubectl get pods -A
```
</p>
</details>


2. Create a new pod with the NGINX image

   <details><summary>Show</summary>
    <p>
    
    ```bash
    kubectl run nginx --image=nginx
    ```
    
    </p>
    </details>
     
  

3. How to find the image of a running pod?
<details><summary>Show</summary>
<p>
    
```bash
kubectl describe pod <podname> 
or 
kubectl get pod <podname> -o yaml
```
</p>
</details>

4. How to find which nodes pods are placed on?
<details><summary>Show</summary>
<p>
    
```bash
kubectl get pods --output wide 
or 
kubectl get pods -o wide
```
</p>
</details>

5. How to find the number of running containers in a pod
<details><summary>Show</summary>
<p>
    
```bash
kubectl get pods and check the READY column
```
</p>
</details>

6. Create a pod with two images nginx and redis (hint: use both imperative command and definition file)
<details><summary>Show</summary>
<p>
    
```bash
kubectl run nginx --image=nginx --dry-run=client -o yaml > pod.yaml
```
edit the pod.yaml
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
  - image: redis
    name: redis
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```
</p>
</details>


7. Create a pod cka with image cka:practice? Is the pod running? What is the state of the pod.
<details><summary>Show</summary>
<p>
    
```bash
kubectl run cka --image=cka:practice
```
The pod is not running. To find out the reason for failure of pod, run
kubectl describe pod cka
you will see that the image is not correct. Delete the pod using 
kubectl delete pod cka

</p>
</details>

8. Delete the pod and recreate with image=consul
<details><summary>Show</summary>
<p>
    
```bash
kubectl run cka --image=consul
```
</p>
</details>

9. Create a pod with image redis using yaml definition file
<details><summary>Show</summary>
<p>
   vim redis.yaml
    
```yaml

apiVersion: v1
kind: Pod
metadata: 
  name: redis
spec: 
  containers:
  - image: redis
    name: redis
```

</p>
</details>
