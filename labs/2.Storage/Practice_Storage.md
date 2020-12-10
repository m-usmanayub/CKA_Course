1. Create a pod with the following definition:


```yaml
apiVersion: v1
kind: Pod
metadata: 
  name: webapp
spec:
  containers:
  - env:
    - name: LOG_HANDLERS
      value: file
    image: kodekloud/event-simulator
    imagePullPolicy: Always
    name: event-simulator
```

2. Check the logs of the pods at /log/app.log. If the pod is deleted will you be able to see the logs?



```bash
kubectl logs webapp
```




3. Configure a volume in the pod to store these logs at /var/log/webapp on the host

Use the spec below:
Name: webapp
Image Name: kodekloud/event-simulator
Volume HostPath: /var/log/webapp
mountPath: /log

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp
spec:
  containers:
  - name: event-simulator
    image: kodekloud/event-simulator
    env:
    - name: LOG_HANDLERS
      value: file
    volumeMounts:
    - mountPath: /log
      name: log-volume

  volumes:
  - name: log-volume
    hostPath:
      # directory location on host
      path: /var/log/webapp
      # this field is optional
      type: Directory
```


4. Create a 'Persistent Volume' with the given specification.
Volume Name: pv-log
Storage: 100Mi
Access modes: ReadWriteMany
Host Path: /pv/log

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-log
spec:
  accessModes:
    - ReadWriteMany
  capacity:
    storage: 100Mi
  hostPath:
    path: /pv/log
```


5. Create a 'Persistent Volume Claim' with the given specification.
Volume Name: pvc-log
Storage Request: 50Mi
Access modes: ReadWriteOnce

```yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: pvc-log
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 50Mi
```


6. What is the state of the Persistent Volume Claim

Pending

7. What is the state of the Persistent Volume

Available

8. Why is the Claim not bound to the available Persistent Volume?

Access Mode MisMatch

9. Update the Access Mode on the claim to bind it to the PVC.

```yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: pvc-log
spec:
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 50Mi
```
Delete and recreate pvc-log

10. You requested for 50Mi, how much capacity is now available to the PVC?
100Mi

11. Update the webapp pod to use the persistent volume claim as its storage.
Replace hostPath configured earlier with the newly created PersistentVolumeClaim
Name: webapp
Image Name: kodekloud/event-simulator
Volume: PersistentVolumeClaim=pvc-log
Volume Mount: /log

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp
spec:
  containers:
  - name: event-simulator
    image: kodekloud/event-simulator
    env:
    - name: LOG_HANDLERS
      value: file
    volumeMounts:
    - mountPath: /log
      name: log-volume

  volumes:
  - name: log-volume
    persistentVolumeClaim:
      claimName: pvc-log
```

12. What is the Reclaim Policy set on the Persistent Volume - 'pv-log' --> Retain

13.  What would happen to the PV if the PVC was destroyed? --> The PV status will be released

14. Try deleting the PVC and notice what happens. --> Terminating Stae

15. Why is the PVC stuck in 'Terminating' state? --> Pod is still using the PVC

16. Delete the 'webapp' Pod. Once deleted, wait for the pod to fully terminate.

17. What is the state of the PVC now?--> Deleted

18. What is the state of the PV now? --> Released
