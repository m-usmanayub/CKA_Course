1. Inspect the environment and identify the authorization modes configured on the cluster.
```bash
kubectl describe pod kube-apiserver-controlplane -n kube-system 
```
    and look for --authorization-mode
    
2. Check the existing roles in the cluster
```bash
kubectl get roles -A
```

3. Check the permissions assigned to the role kube-proxy in the kube-system namespace
```bash
kubectl describe role kube-proxy -n kube-system
```
4. check the rolebinding named kube-proxy and find the account and role in the definition
```bash
kubectl describe rolebinding kube-proxy -n kube-system
```
5. Check if the user faisal created in the previous lab can create pods 
```
kubectl can-i create pod --as faisal
No
```
6. Create a role 'view-only' for the user created in the previous lab with following permissions and bind the user to the role using RoleBinding
    Resources: pods, deployments 
    Action verbs: list, get
```bash
kubectl create role view-only --verb=get --verb=list  --resource=pods,deployments
kubectl create rolebinding view-only-binding --role=view-only 
kubectl can-i create pod --as faisal
```
