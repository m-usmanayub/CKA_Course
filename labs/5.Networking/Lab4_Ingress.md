1. Deploy applications using the apps.yaml file for the lab. 
```bash
kubectl apply -f apps.yaml
```

2. Create the ingress controller using the deploy.yaml file.
```bash
kubectl apply -f deploy.yaml
```

3. Create an ingress resource using the ingress.yaml file
```bash
kubectl apply -f ingress.yaml
```

4. Browse the URLs:  
    NodeIP:NodePort/  
    NodeIP:NodePort/wear  
    NodeIP:NodePort/watch


5. Which namespace is the Ingress Controller deployed in?
   What is the name of the Ingress Controller Deployment?
   Which namespace are the applications deployed in?
   Which namespace is the Ingress Resource deployed in?
   What is the name of the Ingress Resource?

```bash
kubectl get svc -A
kubectl get deploy -A
kubectl get ingress -A
```

6. What is the Host configured on the ingress-resource?
```bash
kubectl get ingress -A
```


7. What backend is the /wear path on the Ingress configured with?
```bash
k describe ingress -n <namespace> <ingress-name>
```

8. At what path is the video streaming application made available on the Ingress?
```bash
k describe ingress -n <namespace> <ingress-name>
```

9. Check the ingress yaml file and change wear path to /clothes.
```bash
kubectl edit ingress -n <namespace> <ingress-name>
```

10. Try to browse by entering any other path and see the output.
```bash
NodeIP:NodePort/test
```

11. Add a new path to the existing ingress to make the food  application available to your customers.
  Ingress: ingress-wear-watch  
  Path: /food  
  Backend Service: food-service  
  Backend Service Port: 8080
```bash
kubectl edit ingress -n <namespace> <ingress-name>
```



12. Make a new application available at path /pay deployed in the critical-space namespace.
Identify and implement the best approach to making this application available on the ingress controller and test to make sure its working. 
Look into annotations: rewrite-target as well.
  Path: /pay  
  Service: pay-service  
  Port: 8282

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-critical
  namespace: critical-space
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /pay
        backend:
          service:
            name: pay-service
            port: 
              name: 8282
```

