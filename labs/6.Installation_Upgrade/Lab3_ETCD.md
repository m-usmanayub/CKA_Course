What is the version of ETCD running on the cluster?

```bash
kubectl logs <etcd-podname> -n kube-system
or 
kubectl describe pod etcd-controlplane -n kube-system
```

At what address do you reach the ETCD cluster from your master/controlplane node?

```bash
kubectl describe pod etcd-controlplane -n kube-system and look for --listen-client-urls
```

Where is the ETCD server certificate file located?
Note this path down as you will need to use it later
```bash
kubectl describe pod etcd-controlplane -n kube-system
```

Where is the ETCD CA Certificate file located?

```bash
/etc/kubernetes/pki/etcd
```

Store the backup file at location /opt/snapshot-pre-boot.db

```bash
ETCDCTL_API=3 etcdctl --endpoints=https://[127.0.0.1]:2379 \
                      --cacert=/etc/kubernetes/pki/etcd/ca.crt \
                      --cert=/etc/kubernetes/pki/etcd/server.crt \
                      --key=/etc/kubernetes/pki/etcd/server.key \
                        snapshot save /opt/snapshot-pre-boot.db
```
Restore the backup from the snapshot taken in previous step
```bash
ETCDCTL_API=3 etcdctl \
     --endpoints=https://[127.0.0.1]:2379 \
     --cacert=/etc/kubernetes/pki/etcd/ca.crt \
     --name=master \
     --cert=/etc/kubernetes/pki/etcd/server.crt --key=/etc/kubernetes/pki/etcd/server.key \
     --data-dir /var/lib/etcd-from-backup \
     --initial-cluster=master=https://127.0.0.1:2380 \
     --initial-cluster-token=etcd-cluster-1 \
     --initial-advertise-peer-urls=https://127.0.0.1:2380 \
     snapshot restore /tmp/snapshot-pre-boot.db
```

Update ETCD POD to use the new data directory and cluster token by modifying the pod definition file at /etc/kubernetes/manifests/etcd.yaml. When this file is updated, the ETCD pod is automatically re-created as this is a static pod placed under the /etc/kubernetes/manifests directory.

Update --data-dir to use new target location
--data-dir=/var/lib/etcd-from-backup

Update new initial-cluster-token to specify new cluster
--initial-cluster-token=etcd-cluster-1

Update volumes and volume mounts to point to new path
```yaml
    volumeMounts:
    - mountPath: /var/lib/etcd-from-backup
      name: etcd-data
    - mountPath: /etc/kubernetes/pki/etcd
      name: etcd-certs
  hostNetwork: true
  priorityClassName: system-cluster-critical
  volumes:
  - hostPath:
      path: /var/lib/etcd-from-backup
      type: DirectoryOrCreate
    name: etcd-data
  - hostPath:
      path: /etc/kubernetes/pki/etcd
      type: DirectoryOrCreate
    name: etcd-certs
```
