1. Deploy the pod color-app using lab definition file 

<details><summary>Show</summary>
<p>

```bash
kubectl apply -f Lab1_Env.yaml
```

</p>
</details>

2. What is the environment variable name and value set on the container in the pod?

<details><summary>Show</summary>
<p>

```bash
APP_COLOR=pink
```

</p>
</details>

3. Browse the URL using node ip and node port

<details><summary>Show</summary>
<p>

```bash
WorkerNodeIP:NodePort
```

</p>
</details>

4. Change the environment variable to GREEN in the pod

<details><summary>Show</summary>
<p>

Change the following line in the definition file to 

```yaml
  - env:
    - name: APP_COLOR
      value: pink
```

</p>
</details>

5. Browse the URL and see if the color changed

<details><summary>Show</summary>
<p>

```bash
WorkerNodeIP:NodePort
```

</p>
</details>
