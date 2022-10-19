# Deployments

## Replication Set

- Replica Set 은 Replication Controller 의 차세대 버전
- Replica Set 은 설정된 값에 의해 필터링 되는 셀렉터를 지원함
    - `environment`에 `dev`나 `qa` 같은 값으로 필터링 가능
    - Replication Controller 와 같이 동일한 것만 찾지 않음
- Replica Set 은 Deployment 객체에 사용됨

## Deployments

- 쿠버네티스에서 Deployment 선언은 애플리케이션의 배포와 업데이트를 수행할 수 있음
- Deployment 객체를 가용한다면 애플리케이션에 상태를 정의할 수 있음
    - 쿠버네티스는 클러스터들을 원하는 상태로 만들기를 보장
- Replication Controller 와 Replica Set 만으로는 애플리케이션을 배포하는데 매우 성가실 수 있음
    - Deployment 객체는 사용하기 쉽고 더 많은 기능들을 제공

- Deployment 객체로 할 수 있는 일
    - Deployment 생성
    - Deployment 수정
    - Rolling Update
    - 이전 버전으로 Roll Back
    - 배포의 중단 및 재개

```yaml
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: helloworld-deployment
spec:
  replicas: 3
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

### Useful Commands
- `kubectl get deployments`
- `kubectl get rs`
- `kubectl get pods --show-labels`
- `kubectl rollout status deployment/helloworld-deployment`
- `kubectl set image deployment/helloworld-deployment k8s-demo=k8s-demo:2`
- `kubectl edit deployment/helloworld-deployment`
- `kubectl rollout status deployment/helloworld-deployment`
- `kubectl rollout history deployment/helloworld-deployment`
- `kubectl rollout undo deployment/helloworld-deployment`
- `kubectl rollout undo deployment/helloworld-deployment --to-revision=n`