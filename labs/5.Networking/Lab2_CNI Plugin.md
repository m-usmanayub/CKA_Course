 ## Lab 2 : CNI Plugin
  
1.  Check the network plugin configured on the cluster
    

  <details><summary>Show</summary>
<p>

```bash
To go /etc/cni/net.d and check the file there.
```

</p>
</details>

2.  Explore the path of the cni plugin for configuration and binary files
    

  <details><summary>Show</summary>
<p>

```bash
Check /opt/cni/bin directory
```

</p>
</details>

3.  How many weave agents are deployed in the cluster
    

  <details><summary>Show</summary>
<p>

```bash
kubectl get pods -n kube-system 
```

</p>
</details>

4.  What is the bridge created by weave
    
<details><summary>Show</summary>
<p>

```bash
ip addr
```

</p>
</details>
  

5.  What is the range of IP addresses configured for PODs on this cluster?
    

  <details><summary>Show</summary>
<p>


The network is configured with weave. Check the weave pods logs using command 
```bash
kubectl logs <weave-pod-name> weave -n kube-system
```
and look for ipalloc-range


</p>
</details>

6.  What is the IP Range configured for the services within the cluster?

<details><summary>Show</summary>
<p>


Inspect the setting on kube-api server by running on command
```bash
cat /etc/kubernetes/manifests/kube-apiserver.yaml | grep cluster-ip-range

```

</p>
</details>
