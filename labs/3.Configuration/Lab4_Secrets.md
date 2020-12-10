1. Check the existing secrets on the cluster

<details><summary>Show</summary>
<p>

```bash
kubectl get secrets
```

</p>
</details>

2. Check the type and data of the existing secrets 

<details><summary>Show</summary>
<p>

```bash
kubectl get secrets
```

</p>
</details>

3. Create a mysql pod with the image=mysql:5.6 and environment variable of:
name: MYSQL_ROOT_PASSWORD
value: password

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata: 
  name: mysql
spec: 
  containers: 
image: mysql:5.6
name: mysql
env: 
- name: MYSQL_ROOT_PASSWORD
  value: password
```

</p>
</details>


4. Expose the pod using service mysql

<details><summary>Show</summary>
<p>

```bash
kubectl expose pod/mysql --name=mysql --target-port=3306 --port=3306
```

</p>
</details>

5. Create a secret containing the data as:
   DB_Server=mysql
   DB_User=root
   DB_Password=password

<details><summary>Show</summary>
<p>

```bash
kubectl create secret generic db-secret --from-literal=DB_Host=mysql --from-literal=DB_User=root --from-literal=DB_Password=password
```

</p>
</details>

6. Create a webapp pod using image kodekloud/simple-webapp-mysql and use the environment variables from the secret created in the previous step.

<details><summary>Show</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    name: webapp-pod
  name: webapp-pod
  namespace: default
spec:
  containers:
  - image: kodekloud/simple-webapp-mysql
    imagePullPolicy: Always
    name: webapp
    envFrom:
    - secretRef:
        name: db-secret
```

</p>
</details>
