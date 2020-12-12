## Lab 5 : DaemonSet

1.  Find out all the DaemonSets running in the cluster in all namespaces.

<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
    

  

2.  Find out the nodes on which DaemonSets are running.
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>

  

3.  Create a DaemonSet in the kube-system namespace using image k8s.gcr.io/fluentd-elasticsearch:1.20 with a resource request of 100m CPU and limit of 200Mi memory.
Mount the following host paths to the container using the same mount path.
/var/log
/var/lib/docker/containers

<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
