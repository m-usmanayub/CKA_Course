How many Namespaces exist on the system?
<details><summary>Show</summary>
<p>

```bash
kubectl get ns
```

</p>
</details>


How many pods exists in research namespace
<details><summary>Show</summary>
<p>

```bash
k get pods -n research
```

</p>
</details>

Create a POD redis in the 'finance' namespace using image redis
<details><summary>Show</summary>
<p>

```bash
k run redis --image=redis --namespace=finance
```

</p>
</details>

Which namespace has the 'blue' pod in it?
<details><summary>Show</summary>
<p>

```bash
k get pods -A
```

</p>
</details>

Access the Blue pod using Node IP and Port.
<details><summary>Show</summary>
<p>

```bash
workerNodeI:NodePort
```

</p>
</details>

What DNS name should the Blue application use to access the database 'db-service' in its own namespace - 'marketing'.
You can try it in the web application UI. Use port 3306.
<details><summary>Show</summary>
<p>

```bash
db-service:3306
```

</p>
</details>

What DNS name should the Blue application use to access the database 'db-service' in the 'dev' namespace. You can try it in the web application UI. Use port 3306.
<details><summary>Show</summary>
<p>

```bash
db-service.dev:3306
```


</p>
</details>
