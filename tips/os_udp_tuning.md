




### UDP Input �� ���õ� �ý��� Ʃ��

------------

UDP�� ���� �ٷ��� ���� ��� syslog�����͸� �����ϴ� ���,UDP Ư���� ��Ŷ drop�� ���� �߻��� �� �ִ�. </br>UDP�� ������ �ս��� ���ֱ�� �������� ������ ���� ������� �ս��� ���� ���� �� �ִ�.</br>

UDP ��Ŷ �ս��� ����� �ֵ� ����.
1.	OS Kernel �������� ���ġ ���� ���� ũ��
�Ϲ� Linux�������� ��ġ�ϸ� Kernel parameter�� ���� �⺻ ���� ���ġ ũ�� �ʱ� ������, �ݵ�� �����ؼ� �÷���� �Ѵ�.
2.	UDP�� �����ϴ� ���ø����̼�(Heavy Forwarder��)�� ����� ������ ó������ ���ϴ� ���
OS���ۿ��� �ش� �޼����� ���ļ� �з������� ���� ���ø����̼ǿ��� �޾ư��� �ϴµ�, ������ �������� ���ϴ� ��쿡�� ��ĥ �� �ִ�.
</br> �⺻������ ���ø����̼� ���μ����� ���� Ʃ���� �ʿ��ϰ�����, Splunk������ buffer ũ�� ���� �� persistentQueue�� enable���Ѽ� ������ ��ȭ�� �� �ִ�.


**OS �������� drop�Ǵ� UDP ��Ŷ�� �� ����͸� ���**

netstat -su �� �����ϸ� �Ʒ��� ���� ����� ���ɴϴ�.?
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
 0 packet receive errors  <-- drop�� ��Ŷ ��
 9427 packets sent
...
```

�ٸ� ���:  splunk���� scripted input���� ���� ������ �ֱ������� �����ؼ� �������� ����͸�
scripted input���� "netstat -su" �� 1�� �ֱ�� �����ؼ� indexing
������ props.conf ���� �ʿ� (�Ʒ��� �����ϰ� �����Ͻø� �� ���մϴ�. �Ϲ����� �����̹Ƿ� ������)

```
SHOULD_LINEMERGE = true
BREAK_ONLY_BEFORE = IcmpMsg
DATETIME_CONFIG = CURRENT
```
�����Ŀ��� "packet receive" �տ� �ִ� ���ڸ� ������ �ʵ� ����.

**OS Parameter ����**
root �������� �Ʒ��� ����
```
sysctl -w net.core.rmem_max=33554432
sysctl -w net.ipv4.udp_mem='262144 327680 393216'
sysctl -w net.core.netdev_max_backlog=2000
```
����ýÿ��� �ݿ��� �� �ֵ��� ���� ������ /etc/sysctl.conf ���Ͽ� �ݿ�


**Splunk���� bufferũ�� �� persistent queue ����**
UDP input�� ������ �ش� inputs.conf ���Ͽ� �Ʒ��Ͱ��� ����
```
 [udp://10541]
��
_rcvbuf = 16777216  �ý����� ��Ĺ���� ��� ����
queueSize = 16MB   ���÷�ũ ���� UDP����
persistentQueueSize = 128MB   ��ũ ����
...
```

_rcvbuf�� OS �� rmem_max���� ���ų� �۾ƾ� ��. </br>
Drop�� 0�� ������ ���� persistentQueue�� 0 ��.. queueSize �� ũ��. </br>
�ʴ� 10Mb ������ ��������. �ʴ� 10MB ? 100Mbps ��. �Ϸ� 1T ��Ʈ�� 144Mbyte  - 1G .. syslogNG </br>

UF  index �� output.conf�� forceTimeBasedAutoLB = true �� �߰��� �ٰ�. </br>?

�����Ʈ:
http://wiki.splunk.com/Community:UDPInputs
https://answers.splunk.com/answers/7001/udp-drops-on-linux.html
http://docs.splunk.com/Documentation/Splunk/6.2.2/Data/SyslogTCP
