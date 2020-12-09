## Lab 4 - ReplicaSet


1. Create a namespace cka-lab4. Perform all the below steps in this namespace.

  <details><summary>Show</summary>
<p>

```bash
k create ns cka-lab4

```
</p>
</details>

2. How many ReplicaSets exist on the system?

  <details><summary>Show</summary>
<p>

```bash
k get rs -A
```
</p>
</details>

3. Create a ReplicaSet using the yaml given for Lab4.

  <details><summary>Show</summary>
<p>

```bash
kubectl apply -f Lab4_ReplicaSet.yaml
```
</p>
</details>

4. How many PODs are DESIRED in the new-replica-set?

  <details><summary>Show</summary>
<p>

```bash
     kubectl get pods 
 
and check the Pods relevant to ReplicaSet
or 
    kubectl get replicaset 
and check the output
```
</p>
</details>

5. What is the image used to create the pods in the new-replica-set?
  <details><summary>Show</summary>
<p>

```bash
kubectl describe replicaset <>
```
</p>
</details>

6. How many PODs are READY in the new-replica-set?
  <details><summary>Show</summary>
<p>

```bash
kubectl get replicaset 
```
</p>
</details>

7. Find out the reason for Pod not ready and fix it.
  <details><summary>Show</summary>
<p>

```bash
Image does not exists. use image busybox or busybox:1.28.4
```
</p>
</details>

8. Delete any one of the pods and see how many are left 
  <details><summary>Show</summary>
<p>

```bash
kubectl delete pod <podname>

A new pod will be immediately created and the number will remain the same as desired by ReplicaSet
```
</p>
</details>

9.  Delete the namespace cka-lab4.
  <details><summary>Show</summary>
<p>

```bash
k delete ns cka-lab4
```
</p>
</details>

