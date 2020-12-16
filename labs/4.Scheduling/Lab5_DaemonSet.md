## Lab 5 : DaemonSet

1.  Find out all the DaemonSets running in the cluster in all namespaces.

<details><summary>Show</summary>
<p>

```bash

kubectl get daemonets --all-namespaces
```

</p>
</details>
    

  

2.  Find out the nodes on which DaemonSets are running.
    
<details><summary>Show</summary>
<p>

```bash

kubectl describe daemonset kube-proxy --namespace=kube-system


```

</p>
</details>

  

3.  Create a DaemonSet in the kube-system namespace using image k8s.gcr.io/fluentd-elasticsearch:1.20 with a resource request of 100m CPU and limit of 200Mi memory.
Mount the following host paths to the container using the same mount path.
/var/log
/var/lib/docker/containers

<details><summary>Show</summary>
<p>

```yaml

apiVersion: apps/v1 #required fields
kind: DaemonSet #required fields
metadata: #required fields
  name: fluentd
  namespace: kube-system
  labels:
    k8s-app: fluentd
spec:
  selector:
    matchLabels:
      name: fluentd #this must match the label below
  template: #required fields 
    metadata:
      labels:
        name: fluentd #this must match the selector above
    spec:
      tolerations:
      - key: node-role.kubernetes.io/master
        effect: NoSchedule
      containers:
      - name: fluentd
        image: k8s.gcr.io/fluentd-elasticsearch:1.20
        resources:
        limits:
          memory: 200Mi
        requests:
          cpu: 100m
        volumeMounts:
        - name: varlog
          mountPath: /var/log
        - name: varlibdockercontainers
          mountPath: /var/lib/docker/containers
          readOnly: true
      volumes:
      - name: varlog
        hostPath:
          path: /var/log
      - name: varlibdockercontainers
        hostPath:
          path: /var/lib/docker/containers

```

</p>
</details>
