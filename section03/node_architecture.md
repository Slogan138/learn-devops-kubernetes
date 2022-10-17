# Node Archtecture

## Architecture Overview

![Architecture Overview](/img/architrcture_overview.png)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nodehelloworld.example.com
  labels:
    app: helloworld
spec:
  containers:
    name: k8-demo
    image: wardviaene/k8s-demo
    ports:
    - containerPort: 3000
```