## Practice Questions - Labels and Annotations


1. Create 3 pods with names nginx1,nginx2,nginx3. All of them should have the label app=v1

  <details><summary>Show</summary>
<p>

```bash
kubectl run nginx1 --image=nginx --restart=Never --labels=app=v1
kubectl run nginx2 --image=nginx --restart=Never --labels=app=v1
kubectl run nginx3 --image=nginx --restart=Never --labels=app=v1

```
</p>
</details>

2. Show all labels of the pods

  <details><summary>Show</summary>
<p>

```bash
kubectl get po --show-labels
```
</p>
</details>

3. Change the labels of pod 'nginx2' to be app=v2

  <details><summary>Show</summary>
<p>

```bash
kubectl label po nginx2 app=v2 --overwrite
```
</p>
</details>

4. Get the label 'app' for the pods (show a column with APP labels)

  <details><summary>Show</summary>
<p>

```bash
kubectl get po -L app
# or
kubectl get po --label-columns=app
```
</p>
</details>

5. Get only the 'app=v2' pods
  <details><summary>Show</summary>
<p>

```bash
kubectl get po -l app=v2
# or
kubectl get po -l 'app in (v2)'
# or
kubectl get po --selector=app=v2
```
</p>
</details>

6. Remove the 'app' label from the pods we created before 
  <details><summary>Show</summary>
<p>

```bash
kubectl label po nginx1 nginx2 nginx3 app-
# or
kubectl label po nginx{1..3} app-
# or
kubectl label po -l app app-
```
</p>
</details>

7. Create a pod that will be deployed to a Node that has the label gpu=nvidia' 
  <details><summary>Show</summary>
<p>

```bash
kubectl label nodes <your-node-name> gpu=nvidia
        
kubectl get nodes --show-labels
```         
```yaml         
apiVersion: v1
kind: Pod
metadata:
  name: cuda-test
spec:
  containers:
    - name: cuda-test
      image: "k8s.gcr.io/cuda-vector-add:v0.1"
  nodeSelector: # add this
    gpu: nvidia # the selection label
```

</p>
</details>

8. Annotate pods nginx1, nginx2, nginx3 with "description='web server'" value 
  <details><summary>Show</summary>
<p>

```bash
kubectl annotate po nginx1 nginx2 nginx3 description='web server'

#or

kubectl annotate po nginx{1..3} description='web server'

```
</p>
</details>

9.  Check the annotations for pod nginx1 
  <details><summary>Show</summary>
<p>

```bash
kubectl describe po nginx1 | grep -i 'annotations'

# or

kubectl get pods -o custom-columns=Name:metadata.name,ANNOTATIONS:metadata.annotations.description

```
</p>
</details>
10.  Remove the annotations for these three pods 
  <details><summary>Show</summary>
<p>

```bash

kubectl annotate po nginx{1..3} description-
```
</p>
</details>



