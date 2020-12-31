Create the resources using the lab definition file.

How many network policies do you see in the environment?
```bash
kubectl get networkpolicy
```

What is the name of the Network Policy?
```
payroll-policy
```

Which pod is the Network Policy applied on?
```
payroll
```

What type of traffic is this Network Policy configured to handle?
```
ingress
```

What is the impact of the rule configured on this Network Policy?
```
traffic from internal to payroll is allowed
```

Perform a connectivity test using the User Interface in these Applications to access the 'payroll-service' at port '8080'.
```
Only internal can access
```

Perform a connectivity test using the User Interface of the Internal Application to access the 'external-service' at port '8080'.
```
allowed
```

Create a network policy to allow traffic from the 'Internal' application only to the 'payroll-service' and 'db-service'
Policy Name: internal-policy
Policy Types: Egress  
Egress Allow: payroll  
Payroll Port: 8080  
Egress Allow: mysql  
MYSQL Port: 3306  

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: internal-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      name: internal
  policyTypes:
  - Egress
  - Ingress
  ingress:
    - {}
  egress:
  - to:
    - podSelector:
        matchLabels:
          name: mysql
    ports:
    - protocol: TCP
      port: 3306

  - to:
    - podSelector:
        matchLabels:
          name: payroll
    ports:
    - protocol: TCP
      port: 8080

  - ports:
    - port: 53
      protocol: UDP
    - port: 53
      protocol: TCP
```
