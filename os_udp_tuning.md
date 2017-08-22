




### UDP Input 에 관련된 시스템 튜닝

------------

UDP를 통해 다량의 보안 장비 syslog데이터를 수집하는 경우,UDP 특성상 패킷 drop이 많이 발생할 수 있다. </br>UDP라서 완전히 손실을 없애기는 힘들지만 다음과 같은 방법으로 손실을 거의 없앨 수 있다.</br>

UDP 패킷 손실이 생기는 주된 이유.
1.	OS Kernel 레벨에서 충분치 않은 버퍼 크기
일반 Linux배포본를 설치하면 Kernel parameter에 대한 기본 값이 충분치 크지 않기 때문에, 반드시 수정해서 늘려줘야 한다.
2.	UDP를 수신하는 어플리케이션(Heavy Forwarder등)이 충분히 빠르게 처리하지 못하는 경우
OS버퍼에서 해당 메세지가 넘쳐서 밀려나가기 전에 어플리케이션에서 받아가야 하는데, 빠르게 동작하지 못하는 경우에는 놓칠 수 있다.
</br> 기본적으로 어플리케이션 프로세스의 성능 튜닝이 필요하겠지만, Splunk에서는 buffer 크기 조정 및 persistentQueue를 enable시켜서 문제를 완화할 수 있다.


**OS 레벨에서 drop되는 UDP 패킷의 양 모니터링 방법**

netstat -su 을 실행하면 아래와 같은 결과가 나옵니다.?
```
netstat -su?
IcmpMsg:
 InType3: 9372
 InType8: 1
 OutType0: 1
 OutType3: 9372
Udp:
 57 packets received
 9372 packets to unknown port received.
 0 packet receive errors  <-- drop된 패킷 수
 9427 packets sent
...
```

다른 방법:  splunk에서 scripted input으로 위의 내용을 주기적으로 수집해서 증가량을 모니터링
scripted input으로 "netstat -su" 를 1분 주기로 실행해서 indexing
적절한 props.conf 설정 필요 (아래와 유사하게 설정하시면 될 듯합니다. 일반적인 내용이므로 생략…)

```
SHOULD_LINEMERGE = true
BREAK_ONLY_BEFORE = IcmpMsg
DATETIME_CONFIG = CURRENT
```
수집후에는 "packet receive" 앞에 있는 숫자를 적절히 필드 추출.

**OS Parameter 수정**
root 계정으로 아래를 수행
```
sysctl -w net.core.rmem_max=33554432
sysctl -w net.ipv4.udp_mem='262144 327680 393216'
sysctl -w net.core.netdev_max_backlog=2000
```
재부팅시에도 반영될 수 있도록 위의 내용을 /etc/sysctl.conf 파일에 반영


**Splunk에서 buffer크기 및 persistent queue 설정**
UDP input을 정의한 해당 inputs.conf 파일에 아래와같이 설정
```
 [udp://10541]
…
_rcvbuf = 16777216  시스템이 소캣별로 잡는 버퍼
queueSize = 16MB   스플렁크 내의 UDP버퍼
persistentQueueSize = 128MB   디스크 버퍼
...
```

_rcvbuf가 OS 의 rmem_max보다 같거나 작아야 함. </br>
Drop을 0로 가져갈 경우는 persistentQueue를 0 로.. queueSize 를 크게. </br>
초당 10Mb 정도면 현실적임. 초당 10MB ? 100Mbps 임. 하루 1T 포트당 144Mbyte  - 1G .. syslogNG </br>

UF  index 로 output.conf에 forceTimeBasedAutoLB = true 를 추가해 줄것. </br>?

참고노트:
http://wiki.splunk.com/Community:UDPInputs
https://answers.splunk.com/answers/7001/udp-drops-on-linux.html
http://docs.splunk.com/Documentation/Splunk/6.2.2/Data/SyslogTCP
