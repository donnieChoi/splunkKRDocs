### dashboard menu 우측 app이름을 icon으로 변경하는 방법
<hr />

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


- 끝

##### 참고자료

https://answers.splunk.com/answers/350493/how-do-i-automatically-build-out-proper-size-icons.html

###  36 x 36</br>

 sips -Z 36 $DOWNLOADS$ICON --out $SPLUNK_APPS$APP/static/appIcon.png </br>
 sips -Z 36 $DOWNLOADS$ICON --out $SPLUNK_APPS$APP/static/appIconAlt.png</br>

 ### 72 x 72
 sips -Z 72 $DOWNLOADS$ICON --out $SPLUNK_APPS$APP/static/appIcon_2x.png</br>
 sips -Z 72 $DOWNLOADS$ICON --out $SPLUNK_APPS$APP/static/appIconAlt_2x.png</br>

 ### 160 x 40
 sips -Z 40 $DOWNLOADS$ICON --out $SPLUNK_APPS$APP/static/appLogo.png</br>

 ### 320 x 80
 sips -Z 80 $DOWNLOADS$ICON --out $SPLUNK_APPS$APP/static/appLogo_2x.png</br>

 
