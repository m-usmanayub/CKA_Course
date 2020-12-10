1. Create a redis pod with redis image that uses emptyDir volume type and mountPath of /data/redis.

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: redis
spec:
  containers: 
  - image: redis
    name: redis
    volumeMounts: 
    - name: data
      mountPath: /data/redis
  volumes: 
  - name: data
    emptyDir: {}
```

</p>
</details>

2. Create busybox pod with two containers, each one will have the image busybox and will run the 'sleep 3600' command. Make both containers mount an emptyDir at '/etc/foo'. Connect to the second busybox, write the first column of '/etc/passwd' file to '/etc/foo/passwd'. Connect to the first busybox and write '/etc/foo/passwd' file to standard output.

<details><summary>Show</summary>
<p>

```bash
kubectl run busybox --image=busybox --restart=Never -o yaml --dry-run=client -- /bin/sh -c 'sleep 3600' > pod.yaml
vi pod.yaml
```
Copy paste the container definition and type the lines that have a comment in the end:
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: busybox
  name: busybox
spec:
  dnsPolicy: ClusterFirst
  restartPolicy: Never
  containers:
  - args:
    - /bin/sh
    - -c
    - sleep 3600
    image: busybox
    imagePullPolicy: IfNotPresent
    name: busybox
    volumeMounts: #
    - name: myvolume #
      mountPath: /etc/foo #
  - args:
    - /bin/sh
    - -c
    - sleep 3600
    image: busybox
    name: busybox2 # don't forget to change the name during copy paste, must be different from the first container's name!
    volumeMounts: #
    - name: myvolume #
      mountPath: /etc/foo #
  volumes: #
  - name: myvolume #
    emptyDir: {} #
```
Connect to the second container:
```bash
kubectl exec -it busybox -c busybox2 -- /bin/sh
cat /etc/passwd | cut -f 1 -d ':' > /etc/foo/passwd 
cat /etc/foo/passwd # confirm that stuff has been written successfully
exit
```
Connect to the first container:
```bash
kubectl exec -it busybox -c busybox -- /bin/sh
mount | grep foo # confirm the mounting
cat /etc/foo/passwd
exit
kubectl delete po busybox
```

</p>
</details>


3. Create an nginx pod using nginx image that uses hostPath as the volume type and /website as the location on host. Create index.html with your name at the location. Mount the volume on the container at /usr/share/nginx/html.Verify the access to the default page. Delete the pod and recreate to see if the same page loads.

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers: 
  - image: nginx
    name: nginx
    volumeMounts: 
    - name: vol
      mountPath: /usr/share/nginx/html
  volumes: 
  - name: vol
    hostPath: 
      path: /website
```

```bash
kubectl exec -it nginx -- /bin/sh
echo "Usman" > /usr/share/nginx/html/index.html

kubectl delete pod nginx 
```
Create the pod again using the same definition file and check if the same homepage opens

</p>
</details>
