 ## Lab 3 : DNS




1. Identify the DNS solution implemented in this cluster.

  <details><summary>Show</summary>
<p>

```bash
kubecl get pods -n kube-system 
```
Check for CoreDNS Pods running

</p>
</details>

2. What service is created for CoreDNS.

  <details><summary>Show</summary>
<p>

```bash
kubectl get svc -n kube-system
```

</p>
</details>

3. What is the IP of the CoreDNS server that should be configured on Pods to resolve services?
  
<details><summary>Show</summary>
<p>

```bash
kubectl get svc -n kube-system and check the service IP
```

</p>
</details>
