# Labels

- Label 은 객체에 key/value 쌍으로 할당할 수 있음
    - AWS 와 같은 클라우드 공급사들의 tag 과 유사
- 조직적인 구조에서 파드들에 label 할 수 있음

```yaml
metadata:
  name: nodehelloworld.example.com
  labels:
    app: helloworld
```

- Labels 는 유일하지 않고 하나의 객체에 여러 label 들을 부여할 수 있음
- 하나의 Label 을 부여하면 필터링 할 때 결곽를 좁힐 수 있음
    - `Label Selectors` 라 명함
- Label Selectors 를 사용하면 맞는 표현식으로 맞는 Labels 를 찾을 수 있음
    
## Node Labels

- Node 들에 대해 또한 Label 을 사용할 수 있음
- Label Selector 를 사용하면 특정 노드에 파드를 실행 시킬 수 있음
- 두 단계로 특정 노드에 파드를 실행 시킬 수 있음
    - 노드에 tag 를 설정함
    - 파드 설정에 `nodeSelector` 를 추가함

1. 노드들에 label 을 정의함

```shell
$ kubectl label nodes node1 hardware=high-spec
$ kubectl label nodes node2 hardware=low-spec
```

2. 파드에 label 을 추가함

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
  nodeSelector:
    hardward: high-spec
```