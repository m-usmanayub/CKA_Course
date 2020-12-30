1. Create a pod using the lab yaml file

```yaml
apiVersion: v1
kind: Pod
metadata:
  Name: sleep-pod
  namespace: default
spec:
  containers:
  - command:
  - sleep
  - "4800"
  image: ubuntu
  imagePullPolicy: Always
  name: ubuntu
```

2. What is the user used to execute the sleep process within the pod?
```
Run the command kubectl exec ubuntu-sleeper -- whoami or run ps aux 
root
```

3. Edit the pod definition to run the sleep process with user ID 1000.
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sleep-pod
  namespace: default
spec:
  securityContext:
    runAsUser: 100
  containers:
  - command:
  - sleep
  - "4800"
  image: ubuntu
  name: ubuntu-sleeper
```
4. Identify the users running the process in the pod definition file

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: multi-pod
spec:
  securityContext:
    runAsUser: 1001
  containers:
  - image: ubuntu
    name: web
    command: ["sleep", "5000"]
    securityContext:
      runAsUser: 1002

  - image: ubuntu
    name: ubuntu
    command: ["sleep", "5000"]
```

5. Try to run the below command in the pod sleep-pod' to set the date. Are you allowed to set date on the POD?
    date -s '31 DEC 2019 12:00:00'

```bash
kubectl exec -it ubuntu-sleeper -- date -s '31 DEC 2019 12:00:00'
```
  no
  
  6. Update pod 'sleep-pod' to run as Root user and with the 'SYS_TIME' capability
```yaml  
apiVersion: v1
kind: Pod
metadata:
  name: sleep-pod
  namespace: default
spec:
  containers:
  - command:
  - sleep
  - "4800"
  image: ubuntu
  name: ubuntu-sleeper
  securityContext:
    capabilities:
      add: ["SYS_TIME"]
```

7. Now try to run the below command in the pod to set the date. If the security capability was added correctly, it should work.
```bash
date -s '31 DEC 2019 12:00:00'
```
kubectl exec -it ubuntu-sleeper -- date -s '31 DEC 2019 12:00:00'
