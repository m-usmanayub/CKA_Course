1. Create a pod ubuntu with image=ubuntu and observe the pod status

<details><summary>Show</summary>
<p>

```bash
kubect run ubuntu --image=ubuntu
```

</p>
</details>

2. Delete and recreate the pod again with command to sleep for 2000 seconds

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: ubuntu
spec:
  containers:
  - name: ubuntu
    image: ubuntu
    command:
      - "sleep"
      - "2000"
```

</p>
</details>

3. Create a pod using the following specs

Pod Name: webapp-color
Image: kodekloud/webapp-color
Command line arguments: --color=green

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webapp-green
  labels:
      name: webapp-green
spec:
  containers:
  - name: simple-webapp
    image: kodekloud/webapp-color
    args: ["--color", "green"]
```

</p>
</details>
