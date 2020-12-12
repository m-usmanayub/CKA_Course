## Lab 4 : Taints and Tolerations

1.  Check the taints on master and worker nodes
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

2.  Create a taint on worker01 with key of ''size”, value of ‘medium’' and effect of 'NoSchedule'
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

3.  Create an nginx pod with the name of nginx-med
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

4.  Is the pod running? Check the status and find the reason
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

5.  How can we make the pod to run? Create another pod with correct definition using image redis and toleration to run on worker node
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

6.  Remove the taint of the master node
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

7.  Check the first pod must be running now on master
    
<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
  

8.  Remove the taint of the worker node and add the taint of the master node back

<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
