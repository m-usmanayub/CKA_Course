## Lab 7 : Updating Deployments

1.  Create a namespace cka-lab20
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

2.  Create a deployment named nginx-deploy in the namespace using nginx image version 1.17 with three replicas and container port 80. Check that the deployment rolled out and show running pods.
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

3.  Expose the deployment using nodePort service and check by browsing the URL.
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

4.  Scale the deployment to 5 replicas and check the status again. Then change the image tag of nginx container from 1.17 to 1.19.
    

  <details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>

5.  Check the history of the deployment and rollback to previous revision. Then check that the nginx image was reverted to 1.17.



<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
