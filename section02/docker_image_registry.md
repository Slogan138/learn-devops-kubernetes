# Docker Image Registry

## Docker

- `docker run` 커맨드를 입력하어 로컬에서 도커 애플리케이션 실행 가능
    - 로컬에서 실행하는 도커는 개발 목적으로 실행
- Kubernetes 에서 활용하는 도커 이미지를 만들기 위해서는 이미지를 도커 레지스트리에 `push` 해야함, ex)Docker Hub
    - 첫번째로 Docker Hub 계정 생성
    - 이후에는 로컬에서 만든 도커 이미지가 저장될 수 있는 도커 레지스트리에 `push` 가능
- Docker Hub에 `push` 하기 위해선 아래 커맨드 참조

```shell
$ docker login
$ docker tag {image_id} {image_name}/{image_tag}
$ docker push {image_name}/{image_tag}
```

- 혹은 이미지 빌드 과정에서 도커 레지스트리에 등록하는 과정은 아래 커맨드와 같음

```shell
$ cd docker-demo
$ docker build -t {image_name}/{image_tag}
$ docker push {image_name}/{image_tag}
```

### 주의사항

- 빌드와 배포를 도커와 쿠버네티스를 사용하려면 몇가지 고려사항이 있음
    - 하나의 컨테이너에는 하나의 프로세스만 실행
        - 하나의 큰 도커 이미지를 만드려고 하지말고, 필요하다면 분할해서 실행
    - 컨테이너의 모든 데이터들은 보존되지 않음, 컨테이너가 종료될때 컨테이너의 모든 변경점은 삭제됨
- [12 factor](https://12factor.net/)를 참조하여 더 많은 팁 확인