# Dummy Date 만들기

<hr />

이런걸 만들고 싶을때가 있다.

![Alt text](https://www.dropbox.com/s/xbwze5tmu3hnxff/Screenshot%202017-09-03%2023.10.22.png?raw=1)

보통은 _internal에서 30일 조회를 하면서 막 date 뽑아서 작업하는데, 이것보다 아래 예제가 훨씬 가볍다.


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
