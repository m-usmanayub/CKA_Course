## Lab 2 : nodeName and nodeSelector

1.  Create a namespace cka-lab15.

<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
    

  

2.  Create a pod using image httpd in the namespace which must be manually scheduled on worker node using nodeName property.
  
<details><summary>Show</summary>
<p>

```yaml
Ans
```

</p>
</details>

  

3.  Label the worker node with size=large
    

  <details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>

4.  Create a pod using nginx image in the lab namespace using nodeSelector property of the podSpec having the value size=large
    

  <details><summary>Show</summary>
<p>

```yaml
Ans
```

</p>
</details>

5.  Delete the namespace cka-lab8 after completing the lab.



<details><summary>Show</summary>
<p>

```bash
Ans
```

</p>
</details>
