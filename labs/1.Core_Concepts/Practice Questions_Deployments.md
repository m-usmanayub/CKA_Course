## Practice Questions - Deployments


1.How many PODs exist on the system?

  <details><summary>Show</summary>
<p>

```bash
kubectl get pods 
  
kubectl get pods -A (for all namespaces)
```
</p>
</details>

2. How many ReplicaSets exist on the system?
  <details><summary>Show</summary>
<p>

```bash
 kubectl get replicasets
 
 kubectl get replicasets --all-namespaces
```
</p>
</details>

3. How many Deployments exist on the system?
  <details><summary>Show</summary>
<p>

```bash

kubectl get deployments

kubectl get deployments --all-namespaces
```
    
</p>
</details>

4. Create a deployment yaml file nginx-deploy having image=nginx:alpine

  <details><summary>Show</summary>
<p>

```bash
kubectl create deployment nginx-deploy --dry-run=client -o yaml > nginx-deploy.yaml
```
</p>
</details>

5. Deploy the yaml definition file using kubectl apply
  <details><summary>Show</summary>
<p>

```bash
kubectl apply -f nginx-deploy.yaml
```
</p>
</details>

6. Scale the deployment to 3 replicas
  <details><summary>Show</summary>
<p>

```bash
kubectl scale deployment nginx-deploy --replicas=3
```
</p>
</details>

7. Check the number of ReplicaSets in the system? How many pods exist now?
  <details><summary>Show</summary>
<p>

```bash
kubectl get replicasets 
```
</p>
</details>

8. Create the deployment using the practice question yaml file for deployment. Fix the issue with the file.
  <details><summary>Show</summary>
<p>

```bash
Fix the kind in the yaml file with Deployment
```
</p>
</details>
