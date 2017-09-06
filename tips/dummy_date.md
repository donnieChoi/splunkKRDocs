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


쪼금 더 나가서.. default 값을 오늘 날자로 박고 싶을때(정적인 값이 아닌 매일 그날의 날자)는 위의 쿼리를 sort하고 selectFirstChoice tag를 써서 해결할 수 있다.

```
<input type="dropdown" token="date01">
     <label>검색일</label>
     <fieldForLabel>workday</fieldForLabel>
     <fieldForValue>workday</fieldForValue>
     <selectFirstChoice>true</selectFirstChoice>
     <search>
       <query>| makeresults
| eval e=relative_time(now(),"-30d@d")
| eval l=relative_time(now(),"+1d@d")
| eval workday=mvrange(e,l,"1d")
| eval workday=strftime(workday,"%Y/%m/%d")
| mvexpand workday
| sort - workday
| table workday</query>
       <earliest>-1d@d</earliest>
       <latest>@d</latest>
     </search>

   </input>
```


이렇게 만든 2017/09/03 같은 값은 그냥 문쟈열일뿐 실제 시간값으로 쓰기 위해서는 하기와 같이 convert 함수를 써서 epoch time 포맷으로 바꾸면 된다.

> | convert timeformat="%Y/%m/%d" mktime(Date01) as D
