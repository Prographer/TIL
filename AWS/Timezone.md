Korea time zone으로 변경

```
[ec2-user@ip-172-31-7-180 ~]$ date
Fri Aug  8 06:41:49 UTC 2014
 
[ec2-user@ip-172-31-7-180 ~]$ sudo date
Fri Aug  8 06:42:01 UTC 2014
 
[ec2-user@ip-172-31-7-180 ~]$ sudo cat /etc/localtime
TZif2UTCTZif2UTC
UTC0
 
[ec2-user@ip-172-31-7-180 ~]$ sudo rm /etc/localtime
 
[ec2-user@ip-172-31-7-180 ~]$ sudo ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime
 
[ec2-user@ip-172-31-7-180 ~]$ date
Fri Aug  8 15:48:27 KST 2014
 
[ec2-user@ip-172-31-7-180 ~]$ sudo date
Fri Aug  8 15:48:40 KST 2014
```