## Lab 3 - Annotations


1.  There is a pod which has the annotation 'author' set to 'Matthew Palmer'.
Find that pod.

  <details><summary>Show</summary>
<p>

```bash
You may use kubectl get pods -o yaml

kubectl describe pods --namespace=cka-lab3 | grep --context=10 'author=Matthew Palmer'
```
</p>
</details>


Edit the pod so that the 'author' annotation is set to your name.

   <details><summary>Show</summary>
    <p>
    
   
    
     kubectl edit pod/pod2 --namespace=cka-lab3

change the annotation name

or use 

     kubectl annotate pod/pod2 --namespace=cka-lab3 author=Usman  --overwrite

    
 </p>
 </details>
     
  
