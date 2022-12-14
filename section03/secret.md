# Secret

- `Secret`은 자격증명, 키, 비밀번호와 같은 보안이 필요한 데이터들을 파드에 배포하는 기능 제공
- 쿠버네티스 자체도 Secret 메커니즘을 활용해 내부 API 에 접근하기 위한 자격 증명을 제공
- 애플리케이션에 동일한 매커니즘을 사용할 수 있음
- Secret 은 다음과 같은 방법으로 사용 가능
    - 환경변수로 사용
    - 파드 안에 파일로 사용
        - 이 경우 컨테이너에 볼륨을 마운트하여 사용
        - 해당 볼륨이 파일을 보유
        - `.env` 파일을 활용해서 애플리케이션에서 읽기만 허용하도록 사용
    - 개인 이미지 저장소에서 외부 이미지를 사용해 시크릿 가져오기

- 파일을 이용해 Secret 생성하는 예

```shell
$ echo -n "root" > ./username.txt
$ echo -n "password" > ./password.txt
$ kubectl create secret generic db-user-pass --from-file=./username.txt --from-file=./password.txt
```

- SSH Key 혹은 SSL 인증으로 사용하기

```shell
$ kubectl create secret generic ssl-certificate --from-file=ssh-privatekey=~/.ssh/id_rsa --from-file=ssl-cert=mysslcert.crt
```

- yaml 파일로 정의하기

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  password: password
  username: username
```

```shell
$ kubectl apply -f secret.yaml
```

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
    env:
    - name: SECRET_USERNAME
      valueFrom:
        secretKeyRef:
          name: db-secret
          key: username
    - name: SECRET_PASSWORD
      valueFrom:
        secretKeyRef:
          name: db-secret
          key: password
```

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
    volumeMounts:
    - name: credvolume
      mountPath: /etc/creds
      readOnly: true
    volumes:
    - name: credvolume
      secret:
      secretName: db-secrets
```