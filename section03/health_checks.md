# Health Checks

- 만약 애플리케이션이 오작동한다면, 파드와 컨테이너는 계속 실행중이지만 애플키레이션은 더이상 동작하지 않음
- `Health checks`를 통해서 애플리케이션을 발견하고 해결할 수 있음
- 2 가지 방법으로 health checks 를 실행할 수 있음
    - 주기적으로 컨테이너에 커맨드를 실행
    - 주기적으로 URL 을 확인
- 로드밸런서 뒤에 동작하는 일반적인 프로덕션 애플리케이션은 health checks 를 구현하여 가용성과 복원력을 보장해야함

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nodehelloworld.example.com
  labels:
    app: helloworld
spec:
  containers:
  - name: k8s-demo
    image: wardviaene/k8s-demo
    ports:
    - containerPort: 3000
    livenessProbe:
      httpGet:
        path: /
        port: 3000
      initialDelaySeconds: 15
      timeoutSeconds: 30
```