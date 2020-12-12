## Lab 3 : Node Affinity

1.  What are the values set to the label beta.kubernetes.io/arch and beta.kubernetes.io/os .
    

<details> <summary> Show </summary>

<p>

```bash
Ans
```

</p>
</details>

  

2.  Apply a label disk=ssd to a worker01 node.
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

3.  Create a new deployment named redis-prod with the redis image and 2 replicas.
    

  <details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>

4.  Where are the pods of the deployment placed on?
    

  <details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>

5.  Set Node Affinity to the deployment to place the pods on worker01 using label assigned above.
    

  <details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>

6.  Check if the pods are placed on worker01 only.
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

7.  Create a new deployment named nginx-prod with the nginx image and 2 replicas, and ensure it gets placed on the master/controlplane node only.Use the label - node-role.kubernetes.io/master - set on the master/controlplane node.

<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
