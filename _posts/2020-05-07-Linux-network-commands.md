---
published: false
---
# 리눅스 네트워크 명령어

- ## ifconfig
네트워크 인터페이스 정보 표시. ip, 브로드캐스트, 서브넷마스크, RX/TX 패킷 등 정보 확인 가능<br />
그냥 ifconfig: 현재 활성화 된 네트워크 인터페이스 (비활성화된 인터페이스를 보기 위해선 -a 옵션 사용)<br />
ifconfig (인터페이스): 해당 인터페이스만 표시<br />
ifconfig (인터페이스) (up 또는 down): 해당 인터페이스 활성화/비활성화<br />
ifconfig (인터페이스) (IP): 해당 인터페이스 IP 편경<br />
<br />
<br />
- ## ip
ifconfig와 비슷하게 IP 정보를 표시하거나 설정<br />
ip (a 또는 addr 또는 address): 네트워크 인터페이스 IP와 기타 정보 표시<br />
ip a add (IP) dev (인터페이스): 인터페이스 IP 추가<br />
ip route: 라우팅 테이블 표시<br />
ip route add (IP/넷마스크) via (게이트웨이): 네트워크 경로 추가<br />
<br />
<br />
- ## netstat
네트워크 인터페이스, 연결 상태, 라우팅 테이블 등 네트워크 정보 표시<br />
netstat: 활성화 된 네트워크 표시<br />
netstat -a: 모든 네트워크 표시<br />
netstat (-t 또는 -u): TCP 또는 UDP 프로토콜만 표시<br />
<br />
<br />
- ## host
호스트의 IP나 도메인을 표시<br />
host (도메인): IP 표시<br />
host (IP): 도메인 표시<br />
<br />
<br />
- ## hostname
호스트 이름 표시하거나 설정<br />
hostname: 호스트네임 표시<br />
hostname (이름): 호스트네임 설정<br />
<br />
<br />
- ## ethtool
이것 역시 네트워크 인터페이스 정보 표시하거나 설정<br />
ethtool (디바이스): 정보 출력<br />
ethtool -s (디바이스) (파라미터): 인터페이스 설정<br />
(예: ethtool -s eth0 autoneg off를 입력하면 eth0 디바이스의 auto-negotiation(speed, duplex 자동 설정) 값이 off로 설정된다.)<br />
<br />
<br />
- ## traceroute
서버까지의 네트워크 경로를 확인<br />
traceroute (도메인 또는 IP)를 입력하면 된다<br />
<br />
<br />
- ## nslookup 
네임서버에 대한 정보 확인<br />
nslookup (도메인 또는 IP)를 입력하면 된다<br />
<br />
<br />
- ## ping
외부 호스트와 연결을 확인<br />
ping (도메인 또는 IP)를 입력하면 된다<br />
<br />