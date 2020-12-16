## Lab : Monitoring

1.  Deploy metrics-server on the Kubernetes Cluster
    
<details><summary>Show</summary>
<p>

```bash
Check the slides for the deployment
```

</p>
</details>
  

2.  Check the nodes and pod CPU and Memory Utilization
    

  <details><summary>Show</summary>
<p>

```bash
kubectl top node 
kubectl top pod
```

</p>
</details>

3.  Find out the Pod with highest CPU utilization and save the pod name in a file cpu.pod at /tmp
    

4.  Find out the pod with lowest memory utilization and save the pod name in a file mem.pod at /tmp
    

5.  Identify the node with highest CPU utilization
    
<details><summary>Show</summary>
<p>

```bash
kubectl top node --sort-by=cpu
```

</p>
</details>
  

6.  Identify the node with highest Memory utilization


<details><summary>Show</summary>
<p>

```bash
kubectl top node --sort-by=memory
```

</p>
</details>
