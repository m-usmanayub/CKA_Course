## Lab 2 - Labels and Selectors


1.How many PODs exist in the 'dev' environment?

<details><summary>Show</summary>
<p>

```bash
kubectl get pods --selector env=dev
```
</p>
</details>


2. How many PODs are in the 'finance' business unit ('bu')?

   <details><summary>Show</summary>
    <p>
    
    ```bash
    kubectl get pods --selector bu=finance
    ```
    </p>
    </details>
     
  3. How many objects are in the 'prod' environment including PODs, ReplicaSets and any other objects?
<details><summary>Show</summary>
<p>
    
```bash
kubectl get all --selector env=prod
```
</p>
</details>

4. Identify the POD which is part of the prod environment, the finance BU and of frontend tier?
<details><summary>Show</summary>
<p>
    
```bash
kubectl get all --selector env=prod,bu=finance,tier=frontend
```
</p>
</details>

