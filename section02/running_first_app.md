# Running First App

- 새롭게 빌드된 애플리케이션을 쿠버네티스 클러스터에 실행해보도록 함
- 컨테이너 기반의 이미지를 실행하기 이전에 `pod definition` 을 만들어야 함
    - pod 는 쿠버네티스에서 실행되는 애플리케이션을 묘사함
    - 파드는 하나 혹은 하나 이상의 컨테이너들을 포함하여 이것들이 애플리케이션을 만듬
        - 앱들이 로컬 포트 번호를 이용해 서로 쉽게 통신할 수 있음

## Create a pod

- 파드를 정의하는 `pod-helloworld.yml` 파일

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
    - conatinerPort: 3000
```

```shell
$ kubectl apply -f pod-helloworld.yml
```

## Usefule Commands

- `kubectl get pod`
- `kubectl descibe pod`
- `kubectl expost pod <pod> --port=444 --name=frontend`
- `kubectl port-forward <pod> 8080`
- `kubectl attatch <podname> -i`
- `kubectl exec <pod> -- command`
- `kubectl label pods <pod> mylabel=awesome`
- `kubectl run -i --tty busybox --image=busybox --restart=Never -- sh`