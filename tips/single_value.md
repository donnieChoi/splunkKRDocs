# Single value Viz Tip
<hr/>

�������� ���� ������ 00�ú��� ���� �ð������� count����(��: call��) �� ����00�ú��� ���ݽð������� call���� ���ϰ� �ʹ�.

���� �����ϰ� ���ٷ� �ذ�ȴ� **special thanks to Mr.Jang**

>| eval event_hour = strftime(_time, "%H%M"), now_hour = strftime(now(), "%H%M")
| where event_hour <= now_hour

��ü�� ��⿡

```
index=idx_voc sourcetype=st_vocmsg
| dedup _raw
| spath CNSL_CD_SEQ
| join CNSL_CD_SEQ
    [ search index=idx_cnsl sourcetype=st_cnsl (MAIN_CNSL_CD=38805 OR MAIN_CNSL_CD=29925)
    | spath TYP_CNSL_CD_NM
    | spath CNSL_CD_SEQ
    | join max=0 TYP_CNSL_CD_NM
        [ inputlookup voc_filter
        | rename VOC_SCAT AS TYP_CNSL_CD_NM ]]
| eval event_hour = strftime(_time, "%H%M"), now_hour = strftime(now(), "%H%M")
| where event_hour <= now_hour
| timechart span=1d count

```

�䷯����ϰ� �ɼǿ��� ������ ����

![compare](https://www.dropbox.com/s/nq2frxibrcdaoon/Screenshot%202017-09-08%2014.20.40.png?raw=1)

![color](https://www.dropbox.com/s/khio5knsozpycfm/Screenshot%202017-09-08%2014.20.50.png?raw=1)

¥��
![result](https://www.dropbox.com/s/7km1z9dxc9wvi3i/Screenshot%202017-09-08%2014.20.59.png?raw=1)


����� �Ҽ��� ������ ���.
### ��
