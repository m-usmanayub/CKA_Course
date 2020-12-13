 ## Lab 1: Cluster Networking
  


1.  Check the network interfaces configured for cluster connectivity and their ip addresses
    

  <details><summary>Show</summary>
<p>

```yaml
ip addr

ip link 

```

</p>
</details>

2.  Check the ports used on the nodes and map to kubernetes services
    

  <details><summary>Show</summary>
<p>

```yaml
ss -ntl
```

</p>
</details>

3.  Explore the YAMLs used for static pods in the master node

<details><summary>Show</summary>
<p>

```yaml
Go to location /etc/kubernetes/manifests/ and see the yaml files
```

</p>
</details>
