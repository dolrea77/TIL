# Load Balancing (로드 밸런싱)



## Load Balancer

- 로드 밸런서란 일반적으로 서버의 부하를 분산 해주는 장치 또는 기술을 뜻함 
- 보통 서버 상단 네트워크에 위치
- 서버 한대에 집증되지 않게 트래픽을 관리하여 각 서버가 최적의 효율을 발휘할 수 있게 해줌 



### Load Balancer 기본 기능

- Health Check : 서버가 정상적으로 작동하고 있는지 체크
- 알고리즘에 따른 분산 처리
- NAT(Network Address Translation)
- DSR(Direct Server Return)



## Load Balancing Algorithm

### Least Connection 알고리즘

- 현재 매핑되어 있는 커넥션이 가장 적은 서버로 세션을 연결해 주는 방식  



### Round Robin 알고리즘

- 들어오는 트래픽을 서버 순서대로 배치하는 방식
- 연결된 세션이 비교적 오래 사용되지 않는 경우에 채택하는 것이 좋음   



### Hash 알고리즘

- 특정 기준을 잡아 특정 서버에 매핑하여 고정적으로 트래픽을 분산해주는 방식
- 일반적으로 사용되는 기준은 출발지(클라이언트)의 IP가 됨  