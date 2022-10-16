# First App with Load Balancer

- 현실에서 시나리오에서는 애플리케이션을 외부에서 접근가능해야 함
- AWS 에서는 외부 로드 밸런서를 쉽게 설정할 수 있음
- AWS 로드 밸런서는 쿠버네티스의 파드에 트래픽을 라우팅할 수 있음
- 로드 밸런서가 없는 다른 클라우드 프로바이더에서는 다른 솔루션을 사용할 수 있음
    - `HAProxy` 혹은 `nginx` 로 클러스터 앞단에 로드 밸런서로 구성할 수 있음
    - 포트를 직접적으로 노출시켜줌

pod: `helloworld.yml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: helloworld
  labels:
    app: helloworld
spec:
  containers:
  - name: k8s-demo
    image: wardviaene/k8s-demo
    ports:
    - name: nodejs-port
      containerPort: 3000
```

service: `helloworld-service.yml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: helloworld-service
spec:
  ports:
  - port: 80
    targetPort: nodejs-port
    protocol: TCP
  selector:
    app: helloworld
  type: LoadBalancer
```