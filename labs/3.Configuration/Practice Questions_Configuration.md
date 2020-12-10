1. Create a pod with the latest busybox image running a sleep for 1 hour, and give it an environment variable named PLANET with the value blue. Then exec a command in the container to show that it has the configured environment variable.

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: envvar
  name: envvar
spec:
  containers:
  - image: busybox:latest
    name: envvar
    args:
    - sleep
    - "3600"
    env:
    - name: PLANET
      value: "blue"
```

```bash
kubectl apply -f envvar.yml
# Check the env variable:
kubectl exec envvar -- env | grep PLANET
PLANET=blue
```

</p>
</details>

2. Create a configmap named space with two values planet=blue and moon=white.
   Create a pod similar to the previous where you have two environment variables taken from the above configmap and show them in the container

<details><summary>Show</summary>
<p>

```bash
kubectl create configmap space --from-literal=planet=blue --from-literal=moon=white
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: envvar
  name: envvar
spec:
  containers:
  - image: busybox:latest
    name: envvar
    args:
      - sleep
      - "3600"
    env:
      - name: PLANET
        valueFrom:
          configMapKeyRef:
            name: space
            key: planet
      - name: MOON
        valueFrom:
          configMapKeyRef:
            name: space
            key: moon
```
```bash
kubectl apply -f envvar.yml
kubectl exec envvar -- env | grep -E "PLANET|MOON"
MOON=white
PLANET=blue
```

</p>
</details>

3. Create a configmap named space-system that contains a file named system.conf with the values planet=blue and moon=white.
   Mount the configmap to a pod and display it from the container through the path /etc/system.conf

<details><summary>Show</summary>
<p>

```bash
cat << EOF > system.conf
planet=blue
moon=white
EOF


kubectl create configmap space-system --from-file=system.conf
cat confvolume.yml
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: confvolume
  name: confvolume
spec:
  containers:
  - image: busybox:latest
    name: confvolume
    args:
      - sleep
      - "3600"
    volumeMounts:
      - name: system
        mountPath: /etc/system.conf
        subPath: system.conf
    resources: {}
  volumes:
  - name: system
    configMap:
      name: space-system
```
```bash
kubectl apply -f confvolume.yml

kubectl exec confvolume -- cat /etc/system.conf
planet=blue
moon=white
```

</p>
</details>

4. Create a secret from files containing a username and a password. Use the secrets to define environment variables and display them. Mount the secret to a pod to credentials folder and display it.

<details><summary>Show</summary>
<p>

```bash
echo -n 'admin' > username
echo -n 'admin-pass' > password

kubectl create secret generic admin-cred --from-file=username --from-file=password
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: secretenv
  name: secretenv
spec:
  containers:
  - image: busybox:latest
    name: secretenv
    args:
      - sleep
      - "3600"
    env:
      - name: USERNAME
        valueFrom:
          secretKeyRef:
            name: admin-cred
            key: username
      - name: PASSWORD
        valueFrom:
          secretKeyRef:
            name: admin-cred
            key: password
```
```bash
kubectl apply -f secretenv.yml

kubectl exec secretenv -- env | grep -E "USERNAME|PASSWORD"
USERNAME=admin
PASSWORD=admin-pass
```
Mount a secret to pod:
```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: secretvolume
  name: secretvolume
spec:
  containers:
  - image: busybox:latest
    name: secretvolume
    args:
      - sleep
      - "3600"
    volumeMounts:
      - name: admincred
        mountPath: /etc/admin-cred
        readOnly: true
  volumes:
  - name: admincred
    secret:
      secretName: admin-cred
```
```bash
kubectl apply -f secretvolume.yml

kubectl exec secretvolume -- ls /etc/admin-cred
password
username

kubectl exec secretvolume -- cat /etc/admin-cred/username
admin

kubectl exec secretvolume -- cat /etc/admin-cred/password
admin-pass
```

</p>
</details>
