## Lab 3-Manual Provisioning and Dynamic Provisioning with Storage Class and Persistent Volume Claim 


1. Create a local StorageClass having name local-sc with the volumeBindingMode set to WaitForFirstConsumer and reclaimPolicy to Delete

  <details><summary>Show</summary>
<p>

```bash
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  annotations:
  name: local-sc
provisioner: kubernetes.io/no-provisioner
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
```
</p>
</details>

2. Create a PV local-pv of size 100Mi using hostPath of /data using the storage class create above and accessMode of RWO
  <details><summary>Show</summary>
<p>

```bash
apiVersion: v1
kind: PersistentVolume
metadata:
  name: local-pv
spec:
  accessModes:
  - ReadWriteOnce
  capacity:
    storage: 100Mi
  hostPath:
    path: /data
  storageClassName: local-sc
```
</p>
</details>

3.  Create a PVC requesting 100Mi of storage using the storageClass as above and accessMode of RWO

  <details><summary>Show</summary>
<p>

```bash
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: local-pvc
spec:
  accessModes:
  - ReadWriteOnce
  storageClassName: local-sc
  resources:
    requests:
      storage: 100Mi
```
</p>
</details>

4.  Check the status of PVC and PV

  <details><summary>Show</summary>
<p>

```bash
kubectl get pv,pvc
```
</p>
</details>

5.. Create an nginx:alpine pod using PVC mounting at /var/www/html and recheck the PVC and PV state

  <details><summary>Show</summary>
<p>

```bash
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:alpine
    volumeMounts:
      - name: local-persistent-storage
        mountPath: /var/www/html
  volumes:
    - name: local-persistent-storage
      persistentVolumeClaim:
        claimName: local-pvc
```
</p>
</details>
