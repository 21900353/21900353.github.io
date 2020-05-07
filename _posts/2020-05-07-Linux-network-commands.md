---
layout: post
title: 리눅스 네트워크 명령어
published: true
---
Describe your Changes
Create 2020-05-07-Linux-network-commands.md
COMMIT
21900353 / 21900353.github.io
_posts/2020-05-07-Linux-network-commands.md
Review your changes:
Additions are highlighted in green. Deletions are crossed out.
---
published: false
---
# 리눅스 네트워크 명령어
<br /><br />
(네트워크를 함부로 설정할 수 없다고 판단해 설정하는 명령어는 설명만 하고 직접 실행하지 못했다. 정보를 표시하는 명령어만 실행했다.)

- ## ifconfig
네트워크 인터페이스 정보 표시. ip, 브로드캐스트, 서브넷마스크, RX/TX 패킷 등 정보 확인 가능<br />
그냥 ifconfig: 현재 활성화 된 네트워크 인터페이스 (비활성화된 인터페이스를 보기 위해선 -a 옵션 사용)<br />
ifconfig (인터페이스): 해당 인터페이스만 표시<br />
ifconfig (인터페이스) (up 또는 down): 해당 인터페이스 활성화/비활성화<br />
ifconfig (인터페이스) (IP): 해당 인터페이스 IP 편경<br />
<br />
![linux3-01.png]({{site.baseurl}}/images/linux3-01.png)<br />
![linux3-01.jpg]({{site.baseurl}}/images/linux3-01.jpg)<br />
ifconfig 실행 결과: 3 개의 활성화된 인터페이스가 있었다. enp129s0f1의 IP 주소는 203.252.112.10 임을 확인할 수 있다.<br />
<br />
![linux3-02.png]({{site.baseurl}}/images/linux3-02.png)<br />
![linux3-02.jpg]({{site.baseurl}}/images/linux3-02.jpg)<br />
ifconfig enp129s0f1 실행 결과: enp129s0f1에 대한 정보만 볼 수 있었다.<br />
<br />
<br />
- ## ip
ifconfig와 비슷하게 IP 정보를 표시하거나 설정<br />
ip (a 또는 addr 또는 address): 네트워크 인터페이스 IP와 기타 정보 표시<br />
ip a add (IP) dev (인터페이스): 인터페이스 IP 추가<br />
ip route: 라우팅 테이블 표시<br />
ip route add (IP/넷마스크) via (게이트웨이): 네트워크 경로 추가<br />
<br />
![linux3-03.png]({{site.baseurl}}/images/linux3-03.png)<br />
![linux3-03.jpg]({{site.baseurl}}/images/linux3-03.jpg)<br />
ip a 실행 결과: 3 개의 활성화된 인터페이스에 대한 정보를 볼 수 있다. ifconfig와는 표시되는 형식이 다르다.<br />
<br />
![linux3-04.png]({{site.baseurl}}/images/linux3-04.png)<br />
![linux3-04.jpg]({{site.baseurl}}/images/linux3-04.jpg)<br />
ip route 실행 결과: 라우팅 테이블이 표시되었다. 기본 경로는 디바이스 enp129s0f1, IP 주소 203.252.112.1에서 시작하고, 다음 경로를 표시한다.<br />
<br />
<br />
- ## netstat
네트워크 인터페이스, 연결 상태, 라우팅 테이블 등 네트워크 정보 표시<br />
netstat: 활성화 된 네트워크 표시<br />
netstat -a: 모든 네트워크 표시<br />
netstat (-t 또는 -u): TCP 또는 UDP 프로토콜만 표시<br />
<br />
![linux3-05.png]({{site.baseurl}}/images/linux3-05.png)<br />
![linux3-05.jpg]({{site.baseurl}}/images/linux3-05.jpg)<br />
netstat -t 실행 결과: TCP 프로토콜로 연결된 네트워크만 표시되었다.<br />
(덧붙이면, netstat -a를 실행했더니 너무 긴 목록이 표시되었다.)<br />
<br />
<br />
- ## host
호스트의 IP나 도메인을 표시<br />
host (도메인): IP 표시<br />
host (IP): 도메인 표시<br />
<br />
![linux3-06.png]({{site.baseurl}}/images/linux3-06.png)<br />
![linux3-06.jpg]({{site.baseurl}}/images/linux3-06.jpg)<br />
www.google.com 과 한동 peace 서버의 IP 주소를 확인할 수 있다.<br />
<br />
<br />
- ## hostname
호스트 이름 표시하거나 설정<br />
hostname: 호스트네임 표시<br />
hostname (이름): 호스트네임 설정<br />
<br />
![linux3-07.png]({{site.baseurl}}/images/linux3-07.png)<br />
![linux3-07.jpg]({{site.baseurl}}/images/linux3-07.jpg)<br />
hostname 실행 결과: 호스트네임이 peace인 것을 확인했다.<br />
<br />
<br />
- ## ethtool
이것 역시 네트워크 인터페이스 정보를 표시하거나 설정<br />
ethtool (디바이스): 정보 출력<br />
ethtool -s (디바이스) (파라미터): 인터페이스 설정<br />
(예: ethtool -s eth0 autoneg off를 입력하면 eth0 디바이스의 auto-negotiation(speed, duplex 자동 설정) 값이 off로 설정된다.)<br />
<br />
![linux3-08.png]({{site.baseurl}}/images/linux3-08.png)<br />
![linux3-08.jpg]({{site.baseurl}}/images/linux3-08.jpg)<br />
ethtool enp129s0f1 실행 결과: 디바이스 enp129s0f1에 대한 설정 정보를 확인했다. Auto-negotiation이 설정되어 있고, 속도는 1000Mb/s이며 Full-duplex이다. 만약 ethtool -s enp129s0f1 speed 100을 입력하면 속도가 100Mb/s 로 변경될 것이다.<br />
<br />
<br />
- ## traceroute
서버까지의 네트워크 경로를 확인<br />
traceroute (도메인 또는 IP)를 입력하면 된다<br />
<br />
![linux3-09.png]({{site.baseurl}}/images/linux3-09.png)<br />
![linux3-09.jpg]({{site.baseurl}}/images/linux3-09.jpg)<br />
traceroute www.google.com 실행 결과: 구글 서버까지 경로가 홉이 13 번 되는 것을 확인했다.<br /> 
(홉: 한 번 라우팅 되는 것을 홉이라 한다)<br />
(* 표시된 것은 타임아웃까지 반응이 없었던 것을 뜻한다)<br />
<br />
<br />
- ## nslookup 
네임서버에 대한 정보 확인<br />
nslookup (도메인 또는 IP)를 입력하면 된다<br />
<br />
![linux3-10.jpg]({{site.baseurl}}/images/linux3-10.jpg)<br />
nslookup www.naver.com 실행 결과: 'Non-authoritative answer' 아래로 네임서버에 대한 정보를 확인했다.<br /> 
<br />
<br />
- ## ping
외부 호스트와 연결을 확인<br />
ping (도메인 또는 IP)를 입력하면 된다<br />
<br />
![linux3-11.jpg]({{site.baseurl}}/images/linux3-11.jpg)<br />
ping www.daum.net 실행 결과: 기다려도 아무 반응이 없어서 Ctrl+c로 종료하자 100% packet loss라고 나왔다. 단 하나의 패킷도 반응이 없었다는 것은 연결이 되지 않았다는 말이다.<br /> 
<br />
Prose