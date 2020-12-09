## Practice Questions - ReplicaSet


1. Deploy the ReplicaSet using 2_PracticeQS_RS1.yaml. Check if the deployment is successful. Fix the issue and deploy again.

  <details><summary>Show</summary>
<p>

```bash
kubectl explain rs | grep VERSION


```
</p>
</details>

2. Deploy the ReplicaSet using 2_PracticeQS_RS2.yaml. Check if the deployment is successful. Fix the issue and deploy again.
  <details><summary>Show</summary>
<p>

```bash
Match the labels on the selector and pod template in the defintion file
```
</p>
</details>

3. Scale the 1st ReplicaSet to 5 PODs. Use 'kubectl scale' command or edit the replicaset using 'kubectl edit replicaset'.

  <details><summary>Show</summary>
<p>

```bash
kubectl edit replicaset new-replica-set 

or 
  
kubectl scale rs replicaset-1 --replicas=5
```
</p>
</details>

4. Now scale the ReplicaSet down to 2 PODs.

  <details><summary>Show</summary>
<p>

```bash
kubectl scale replicaset replicaset-1 --replicas=2
```
</p>
</details>
