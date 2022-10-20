# Services

- 쿠버네티스 클러스터에서 파드들은 매우 동적임
    - Replication Controller 를 사용할 때 파드들은 크기를 변경하는 명령중에 삭제되고 생성됨
    - Deployment 를 사용하면 이미지 버전을 업데이트할 댸 파드들은 오래된 파드들이 삭제되고 새로운 파드들로 교체됨
- 이러한 이유들 때문에 파드들에 직접 접근하면 안되고 서비스를 통해 접근해야함
- 서비스는 사라질 수 있는 파드들과 다른 서비스 혹은 사용자들 간의 논리적 다리
- `kubectl expose` 커맨드를 통해 파드에 새로운 서비스를 생성하면 외부와 통신이 가능해짐
- 파드들에 새로운 엔드포인트를 생성할 수 있는 방법
    - ClusterIP: 클러스터에 도달할 수 있는 가상 IP 주소(default)
    - NodePort: 외부에서 각 노드에 통신할 수 있는 포트
    - LoadBalancer: 클라우드 공급자에 의해 생성되어 NodePort에 외부 트래픽을 라우팅 해줌
- DNS names 를 사용할 수 있음
    - ExternalName 은 서비스에 DNS 이름을 제공

```yaml
apiVersion: v1
kind: Service
metadata:
  name: helloworld-service
spec:
  ports:
  - port: 31001
    nodePort: 31001
    targetPort: nodejs-port
    protocol: TCP
  selector:
    app: helloworld
  type: NodePort
```