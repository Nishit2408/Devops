# Following rules make kubernetes cluster secure

**1) Prevent containers from escalating privileges**

**Rule impact:**
  In their default state, containers allow privilege escalation. Attackers may use this to manipulate the application and to gain more permissions than       they should have
    
**How to fix this failure:**
  Missing key `allowPrivilegeEscalation` - set to false to prevent attackers from exploiting escalated container privileges
    
    **Example**
    ```
    kind: Deployment
    spec:
      template:
        spec:
          containers:
            - name: myContainer
              securityContext:
                allowPrivilegeEscalation: false
     ```
     
**2) Ensure each container has a read-only root filesystem** 
    
**Rule impact:**
  An immutable root filesystem prevents attackers from being able to tamper with the filesystem or write foreign executables to disk
  
**How to fix this failure:**
Incorrect value for key `readOnlyRootFilesystem` - set to 'true' to protect filesystem from potential attacks  

**Example**
Set the ```readOnlyRootFilesystem``` key with a value of true either at pod level or container level:

```
kind: Pod
spec:
  securityContext:
    readOnlyRootFilesystem: true
```

```
kind: Deployment
spec:
  containers:
    - name: myContainer
      securityContext:
        readOnlyRootFilesystem: true
```

**3) Ensure each container has a read-only root filesystem**

**Rule impact:**
An immutable root filesystem prevents attackers from being able to tamper with the filesystem or write foreign executables to disk


**How to fix this failure:**
Incorrect value for key `readOnlyRootFilesystem` - set to 'true' to protect filesystem from potential attacks

**Example**
Set the readOnlyRootFilesystem key with a value of true either at pod level or container level:

```
kind: Pod
spec:
  securityContext:
    readOnlyRootFilesystem: true
```
```
kind: Deployment
spec:
  containers:
    - name: myContainer
      securityContext:
        readOnlyRootFilesystem: true
```

**4) Prevent containers from escalating privileges**

**Rule impact:**
In their default state, containers allow privilege escalation. Attackers may use this to manipulate the application and to gain more permissions than they should have


**How to fix this failure:**
Missing key `allowPrivilegeEscalation` - set to false to prevent attackers from exploiting escalated container privileges

**Example**

```
kind: Deployment
spec:
  template:
    spec:
      containers:
        - name: myContainer
          securityContext:
            allowPrivilegeEscalation: false
```            

**4) Ensure Deployment has more than one replica configured**

**Rule impact:**
When running two or more replicas per service, you are increasing the availability of the containerized service by not relying on a single pod to do all of the work

**How to fix this failure:**
Incorrect value for key `replicas` - running 2 or more replicas will increase the availability of the service

**Example**

```
kind: Deployment
spec:
  replicas: 2
```  

**5) Ensure each container has a configured readiness probe**

**Rule impact:**
Readiness probes allow Kubernetes to determine when a pod is ready to accept traffic. This ensures that client requests will not be routed to pods that are unable to process them

**How to fix this failure:**
Missing property object `readinessProbe` - add a properly configured readinessProbe to notify kubelet your Pods are ready for traffic

**Example:**

```
spec:
  containers:
    - name: app
      image: nginx:1.19.8
      readinessProbe:
        httpGet:
          path: /healthz
          port: 8080
```
```
spec:
  containers:
    - name: app
      image: nginx:1.19.8
      readinessProbe:
        tcpSocket:
          port: 8080
```
```
spec:
  containers:
    - name: app
      image: nginx:1.19.8
      readinessProbe:
        exec:
          command:
            - cat
            - /tmp/healthy
```

**6) Ensure each container has a configured liveness probe**

**Rule impact:**
When liveness probes aren't set, Kubernetes can't determine when a pod should be restarted, which can result with an unavailable application

**How to fix this failure:**
Missing property object `livenessProbe` - add a properly configured livenessProbe to catch possible deadlocks

**Example:**
Configure a liveness probe with an HTTP request, TCP protocol or exec command (the least recommended option)

```
spec:
  containers:
    - name: app
      image: nginx:1.19.8
      livenessProbe:
        httpGet:
          path: /healthz
          port: 8080
```
```
spec:
  containers:
    - name: app
      image: nginx:1.19.8
      livenessProbe:
        tcpSocket:
          port: 8080
```
```
spec:
  containers:
    - name: app
      image: nginx:1.19.8
      livenessProbe:
        exec:
          command:
            - cat
            - /tmp/healthy
```            






   


