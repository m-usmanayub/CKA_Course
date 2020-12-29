## Lab 1 

1. Create a CSR for a new user named faisal
```bash
openssl genrsa -out faial.key 2048
openssl req -new -key faisal.key -subj "/CN=faisal" -out faisal.csr 
```

2. Create a CertificateSigningRequest object with the name faisal with the contents of the faisal.csr file
```bash
cat faisal.csr | base64 | tr -d "\n"
```
```yaml
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: john
spec:
  groups:
  - system:authenticated
  request: LS0tLS1CRUdJTiBDR……….(output omitted)
  signerName: kubernetes.io/kube-apiserver-client
  usages:
  - client auth
  ```
  
  3. Verify the CSR is created and check its state
  ```bash
  kubectl get csr
  ```
  
  4. Approve the CSR. 
  
 ```bash
 kubectl certificate approve faisal
 ```
 
 5. Use the certificate to add the user into the kubeconfig file
 
 
 6. Create a service account named jenkins
 ```bash
kubectl create serviceaccount jenkins
```
