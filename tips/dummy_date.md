# Dummy Date �����

<hr />

�̷��� ����� �������� �ִ�.

![Alt text](https://www.dropbox.com/s/xbwze5tmu3hnxff/Screenshot%202017-09-03%2023.10.22.png?raw=1)

������ _internal���� 30�� ��ȸ�� �ϸ鼭 �� date �̾Ƽ� �۾��ϴµ�, �̰ͺ��� �Ʒ� ������ �ξ� ������.


```
| makeresults
| eval e=relative_time(now(),"-30d@d")
| eval l=relative_time(now(),"+1d@d")
| eval workday=mvrange(e,l,"1d")
| eval workday=strftime(workday,"%Y/%m/%d")
| mvexpand workday
| table workday
```


![Alt text](https://www.dropbox.com/s/04henvbukmqpiec/Screenshot%202017-09-06%2015.45.48.png?raw=1)
