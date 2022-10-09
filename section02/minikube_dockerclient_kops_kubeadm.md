# Minikube vs. Docker Client vs. kops vs. kubeadm

- 쿠버네티스 클러스터를 설치할 수 있는 여러 도구
    - Minukube
    - Docker Client
    - kops
    - kubeadm
- minikube 혹은 docker client 을 이용해 로컬에 설치
- 실제 프로덕션 클러스터를 설치하기 위해서는 다른 방법을 사용해야함
    - minikube, docker client 는 로컬에 설치하기 매우 편리함, 그러나 실제 클러스터를 위함은 아님
    - kops, kubeadm 은 프로덕션 클러스터를 설치하기 위한 툴

- AWS 에서는 kops 가 최적의 툴
    - AWS EKS 사용해도 가능, 가장 선호되는 옵션
- kops 를 사용하지 못한다면 kubeadm 을 활용할 수 있음
    - kubeadm 은 좀 더 일반적인 접근