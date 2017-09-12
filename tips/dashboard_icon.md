# Splunk Look&Feel Customization

<hr />

### Login화면의 splunk> 이미지 변경

1. $SPLUNK_HOME/etc/apps/search/appserver/static/ 하기에 logincustomlogo 디렉토리 생성 후 변경할 image를 넣어놓는다.

2. $SPLUNK_HOME/etc/system/local/web.conf 에 해당 이미지 경로 넣기
<br />

```
[root@localhost local]# cat web.conf
[settings]
loginCustomLogo = logincustomlogo/<image>.png
```

3. restart

<hr/>
### Login 화면의 배경화경 변경


admin 으로 로그인 후, 설정 --> 서버 설정 --> 로그인 배경

![background](https://www.dropbox.com/s/edpcts1g4f05uor/Screenshot%202017-09-12%2009.37.27.png?raw=1)

1024x768이상의 해상도를 가진 이미지를 권고한다.


<hr />
### App 의 icon변경


dashboard menu 의 우측 app 이름,app menu을 아이콘으로 변경하는 방법.


- 하기와 같이 $SPLUNK_HOME/etc/apps/<해당app>/static 디렉토리에 변경할 image 파일을 알맞게 resize 하여 넣은 후
```
schoi@seungdons-MacBook-Pro ~/Documents/instances/660/etc/apps/seungdon/static (master*) $ ls -lrt
total 64
-rwxr-xr-x  1 schoi  staff  7709 May 29 08:47 appLogo_2x.png
-rwxr-xr-x  1 schoi  staff  7709 May 29 08:47 appLogo.png
-rwxr-xr-x  1 schoi  staff  7966 May 29 08:47 appIconAlt_2x.png
-rwxr-xr-x  1 schoi  staff  7966 May 29 08:47 appIconAlt.png
```


- splunksh:8000/debug/refresh 에 접속하여  refresh 버튼 클릭하여 cache를 refresh시켜줍니다.

사용하는 아이콘의 사이즈는 하기와 같이 지정해 주도록 한다.
1. 36 x 36

 SPLUNK_APPS/APP/static/appIcon.png </br>
 SPLUNK_APPS/APP/static/appIconAlt.png</br>

2. 72 x 72
 SPLUNK_APPS/APP/static/appIcon_2x.png</br>
 SPLUNK_APPS/APP/static/appIconAlt_2x.png</br>

3. 60 x 40
 SPLUNK_APPS/APP/static/appLogo.png</br>

4. 320 x 80
 SPLUNK_APPS/APP/static/appLogo_2x.png</br>




##### 참고자료

https://answers.splunk.com/answers/350493/how-do-i-automatically-build-out-proper-size-icons.html
