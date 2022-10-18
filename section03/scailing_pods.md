# Scailing Pods

## Scailing

- 만약 애플리케이션이 상태가 없다면 수평적으로 확장할 수 있음
    - Stateless(상태가 없는): 애플리케이션이 상태를 가지지 않는 것, 로컬 파일을 쓰지 않고 로컬 세션을 유지함
    - 전통적인 모든 데이터베이스들(MySQL, Postgres)은 상태를 가짐, 여러 인스턴스에 나눠 저장할 수 없는 데이터베이스 파일들을 가지고 있음
- 대부분의 웹 애플리케이션은 상태가 없게 만들 수 있음
    - 세션 관리는 컨테이너 외부에서 이루어져야 함, Memcached나 Redis 같은 서비스를 이용
    - 저장되어야 하는 모든 파일들은 컨테이너 내부에서 저장 할 수 없음, 컨테이너를 재시작하면 변경사항들이 모두 사라지기 때문

- 쿠버네티스에서의 확장은 `Replication Controller`를 통해 가능
- Replication Controller 는 모든 상황에서 지정된 숫자의 파드 레플리카들을 실행되도록 함
- Replication Controller 를 통해 파드가 생성되었다면 실패, 삭제, 파괴되었을 때 자동적으로 교체됨
- 재부팅 이후에도 1개의 파드를 항상 실행하려고 할 때 Replication Controller 로의 실행이 권장됨
    - 이 경우 Replication Controller 는 1개의 레플리카를 생성
    - 파드가 항상 동작중임을 확실히 할 수 있음

```yaml
apiVersion: v1
kind: ReplicationController
metadata:
  name: helloworld-controller
spec:
  replicas: 2
  selector:
    app: helloworld
  template:
    metadata:
      labels:
        app: helloworld
    spec:
      containers:
      - name: k8s-demo
        image: wardviaene/k8s-demo
        ports:
        - containerPort: 3000
```