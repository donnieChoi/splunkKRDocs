### dashboard menu ���� app�̸��� icon���� �����ϴ� ���
<hr />

- �ϱ�� ���� $SPLUNK_HOME/etc/apps/<�ش�app>/static ���丮�� ������ image ������ �˸°� resize �Ͽ� ���� ��
```
schoi@seungdons-MacBook-Pro ~/Documents/instances/660/etc/apps/seungdon/static (master*) $ ls -lrt
total 64
-rwxr-xr-x  1 schoi  staff  7709 May 29 08:47 appLogo_2x.png
-rwxr-xr-x  1 schoi  staff  7709 May 29 08:47 appLogo.png
-rwxr-xr-x  1 schoi  staff  7966 May 29 08:47 appIconAlt_2x.png
-rwxr-xr-x  1 schoi  staff  7966 May 29 08:47 appIconAlt.png
```


- splunksh:8000/debug/refresh �� �����Ͽ�  refresh ��ư Ŭ���Ͽ� cache�� refresh�����ݴϴ�.


- ��

##### �����ڷ�

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

 
