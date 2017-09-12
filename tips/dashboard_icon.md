# Splunk Look&Feel Customization

<hr />

### Loginȭ���� splunk> �̹��� ����

1. $SPLUNK_HOME/etc/apps/search/appserver/static/ �ϱ⿡ logincustomlogo ���丮 ���� �� ������ image�� �־���´�.

2. $SPLUNK_HOME/etc/system/local/web.conf �� �ش� �̹��� ��� �ֱ�
<br />

```
[root@localhost local]# cat web.conf
[settings]
loginCustomLogo = logincustomlogo/<image>.png
```

3. restart

<hr/>
### Login ȭ���� ���ȭ�� ����


admin ���� �α��� ��, ���� --> ���� ���� --> �α��� ���

![background](https://www.dropbox.com/s/edpcts1g4f05uor/Screenshot%202017-09-12%2009.37.27.png?raw=1)

1024x768�̻��� �ػ󵵸� ���� �̹����� �ǰ��Ѵ�.


<hr />
### App �� icon����


dashboard menu �� ���� app �̸�,app menu�� ���������� �����ϴ� ���.


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

����ϴ� �������� ������� �ϱ�� ���� ������ �ֵ��� �Ѵ�.
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




##### �����ڷ�

https://answers.splunk.com/answers/350493/how-do-i-automatically-build-out-proper-size-icons.html
