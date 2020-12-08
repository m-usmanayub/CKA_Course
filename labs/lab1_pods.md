## Lab 1 - Pods

1. Create a namespace called cka-lab1 in your cluster.

<details><summary>Show</summary>
<p>

```bash
kubectl create namespace cka-lab1
```

</p>
</details>

2. Run the following pods in this namespace.

    a. A pod called pod-a with a single container running the nginx image. 
    
    <details><summary>Show</summary>
    <p>
    
    ```bash
    k run pod-a --image=nginx --namespace=cka-lab1
    ```
    
    </p>
    </details>
     
    b. A pod called pod-b that has one container running the image redis:alpine, and one container running nginx:alpine. 
      
    <details><summary>Show</summary>
    <p>
    
    ```bash
    kubectl  run pod-b --image=nginx --namespace=cka-lab1 --dry-run=client -o yaml > pod-b.yaml
    ```
    
    </p>
    </details>

3. Write down the output of `kubectl get pods` for the kube-system namespace.
<details><summary>Show</summary>
<p>
    
```bash
kubectl get pods --namespace kube-system
```
</p>
</details>

4. Delete the namespace cka-lab1


<details><summary>Show</summary>
<p>
    
```bash
kubectl delete ns cka-lab1
```
</p>
</details>



