# Kops

- AWS 에 쿠버네티스를 설치하려면 kops 를 사용하면 편리함
    - kops 는 Kubernetes Operations 의 약자
- 프로덕션 레벨의 쿠버네티스 클러스터 설치, 업그레이드, 관리를 위한 툴
- `kube-up.sh` 이라 불리우는 레거시 툴도 존재
- kops 는 리눅스 혹은 맥에서만 동작
- 윈도우 사용자라면 리눅스 가상 머신이 필요
- Vagrant 를 이용해서 빠르게 리눅스 환경 구축 가능
- 단지 설치 후 아래의 커맨드만 실행하면 됨

```shell
$ vagrant init ubuntu/xenial64
$ vagrant up
```