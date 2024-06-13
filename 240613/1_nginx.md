## Nginx Gateway API - Ingress

* DB에도 LB를 구성해서 사용하는 방법을 구성할 수 있음
* Service별로 Loadbalancer를 태우는게 비효율적
  > 각각의 Service마다 LoadBalance를 만드는게 문제여서 Ingress를 씀
* Ingress가 여러 Service를 백엔드에 둘 수 있음

* Ingress는 리소스
* Ingress Controller는 실제 트래픽을 처리
  > 설정의 경우 API로 처리

* L7(Ingress Controller) -> L4(Service) -> POD

(1) K8s G/W API
* Ingress API 개선 요건이 있음
* NGINX CRD
  > 제조사 CRD를 맡김
* 종속성 문제를 해결
  > Gateway API
* Annotation 문제
  > 실제 설정하는 구문이 많아짐
  > 관리 문제가 생김
  > 단일 Namespace만 쓸수밖에 없음(Ingress가)
* gateway api
  > 2023.10에 GA
  > 역할기반 모델
  > API : gateway.networking.k8s.io
* Gateway Class
  > 생성하는 스펙, 인프라 관리자
* Gateway
* Route
* 빠르게 Ingress를 대체할 수 있음

(2) Nginx Gateway Fabric
* Nginx는 성능이 좋음
* 확장성이 좋음
  > Non-Annotation
* 모든 플랫폼에서 구성 가능
* Gateway API가 여러 기능들이 압도적으로 좋음(Ingress와 제조사 API 대비)
  > L4(TCP/UDP)도 지원함
* 사용자 지정정책은 곧 지원될 예정임
  > 지난달 1.1 버전이 나옴

(3) N-S 트래픽 라우팅
* Gateway는 Listener이다.
* Github Repository URL
  > https://github.com/nginxinc/nginx-gateway-fabric
* 환경은 가벼워서 Docker Desktop에 K8s 띄어서 진행
* 반드시 Service를 거쳐서 POD로 보냄
* Route는 여러 종류를 사용할 수 있음
  > HTTPRoute
* Gateway 단에서 도메인 매칭에 대한 설정을 통해 리스너 처럼 제어 할 수 있음
  > Route도 마찬가지 이다.
* https://github.com/nginxinc/nginx-gateway-fabric/tree/main/examples/cafe-example

(4) HTTP 트래픽 분할
* Traffic-spiltting
  > 호스트네임을 넣으면 호스트매칭
  > 없으면 포트매칭으로만
* Weight 설정을 할 수 있음
  > Weight를 적어도 똑같은 비율로 나뉨
* https://github.com/nginxinc/nginx-gateway-fabric/tree/main/examples/traffic-splitting

(5) 속성기반 라우팅
* Parameter 라우팅이 가능해짐
* https://github.com/nginxinc/nginx-gateway-fabric/tree/main/examples/advanced-routing
* 파라메터를 줄 경우 라우팅이됨
  > 가령 v2를 주면 v2 서비스쪽으로
* 호스트 헤더에 줘도 라우팅을 할 수 있음

(6) 메소드 기반 라우팅
* https://github.com/nginxinc/nginx-gateway-fabric/tree/main/examples/advanced-routing

(7) 정리
* Ingress 제약사항 때문에 확장된 API
* 서비스 디스커버리 및 서비스 메시등과 호환 가능
* 특정 Gateway에 종속되지 않음
* Nginx Gateway Fabric은 1.3.0이 나옴



  
