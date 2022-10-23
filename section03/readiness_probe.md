# Readiness Probe

- livenessProbes 와 같이 컨테이너에 readinessProbe 를 사용할 수 있음
- livenessProbes: 컨테이너의 실행 여부를 확인
    - 실패 상태일 때 컨테이너는 재시작 됨
- readinessProbes: 컨테이너가 요청 처리를 대기중인지 확인
    - 실패 상태일 때 컨테이너는 재시작되지 않지만 파드의 IP 주소가 서비스에서 사라지면서 더 이상 요청을 처리하지 않음
- readiness 테스트는 시작 시 테스트가 성공했을 떄만 파드가 트래픽을 수신하는지 확인
- Probe 들을 함께 사용할 수 있고 다른 테스트를 설정할 수 있음
- 컨테이너가 무언가 잘못 되었을때 종료된다면 livenessProbe 는 필요하지 않음
- 보통의 경우 livenessProbe 와 readinessProbe 를 같이 구성하여 사용