## Lab 2 - Persistent Volume and Persistent Volume Claim


1. First, create a Persistent Volume resource in your cluster. It should be called storage-lab-pv, allow for 1Gi of storage capacity, be of type hostPath on host /data/pv, and allow for ReadWriteOnce access.

  <details><summary>Show</summary>
<p>

```bash
kind: PersistentVolume
apiVersion: v1
metadata:
  name: storage-lab-pv
spec:
  hostPath:
    path: /data/pv
  accessModes:
    - ReadWriteOnce
  capacity:
    storage: 1Gi


```
</p>
</details>

2. 1.  Second, create a Persistent Volume Claim in your cluster that makes a request for this Persistent Volume resource. It should be called storage-lab-pvc and needs to request 512Mi storage.
  <details><summary>Show</summary>
<p>

```bash
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: storage-lab-pvc
spec:
  resources:
    requests:
      storage: 512Mi
  accessModes:
    - ReadWriteOnce
```
</p>
</details>

3.  Third, create a Pod in your cluster that can use this persistent volume.It should be called storage-lab-pod, run the nginx:1.16 image, and mount the persistent volume at /etc/storage-lab-data.

  <details><summary>Show</summary>
<p>

```bash
kind: Pod
apiVersion: v1
metadata:
  name: storage-lab-pod
spec:
  volumes:
    - name: lab-vol
      persistentVolumeClaim:
        claimName: storage-lab-pvc
  containers:
    - name: nginx
      image: nginx:1.16
      volumeMounts:
        - name: lab-vol
          mountPath: /etc/storage-lab-data
```
</p>
</details>


