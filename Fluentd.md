#개요
Fluentd는 Log를 수집 하는 프로그램이다. 루비로 제작되었으며, 성능 이슈가 있는 라이브러리는 C를 이용하여 제작 되었다.  
in, out을 설정하여 fluentd -> fluentd -> db,file등 구조등 다양하게 설정이 가능하다.  

#설치

## 설치전 환경 설정. [link](http://docs.fluentd.org/articles/before-install)

1. NTP를 설정해야 한다. 
2. Max file 개수를 지정해야 한다.
3. Network parameter를 최적화 해야 한다.

## 설치방법
```
curl -L https://toolbelt.treasuredata.com/sh/install-redhat-td-agent2.sh | sh
```

## 실행등록
```
chkconfig td-agent on
```

## 환경설정

### 단일설정
```
<source>
  type forward
  port 24224
  tag log.test
</source>

<match *.*>
  type stdout
</match>
```

### java -> fluentd -> fluentd -> s3 연결

1. java
```
//static 변수 설정
private static FluentLogger viewCountLogger = FluentLogger.getLogger("s3.logs.ad");

//함수에서 
viewCountLogger.log("view", ObjectUtil.toMap(adData));

//tag값이 s3.logs.ad.view로 설정된다. 이 태그 값은 match에 설정시 사용한다.
```

2. java와 같은 머신의 fluentd의 환경설정
```
<source>
  type forward
  port 24224
</source>

<match s3.logs.ad.*>
  type forward

  <server>
    name logserver
    host xxx.xxx.xxx.xxx
    port 24224
  </server>

  #환경설정은 http://docs.fluentd.org/articles/out_forward 에서 확인 가능
  flush_interval 1
  send_timeout 60
  heartbeat_type udp
  heartbeat_interval 1
  recover_wait 10
  hard_timeout 60
  expire_dns_cache nil
  phi_threshold 16
  phi_failure_detector true

</match>

```
3. 로그 서버에서 s3로 전송하는 fluentd 환경 설정
```
<source>
  type forward
  port 24224
  bind 0.0.0.0
</source>

<match s3.logs.ad.*>
  type s3

  aws_key_id xxxxxxxxxxxx
  aws_sec_key xxxxxxxxxxxxxx
  s3_bucket bucket_name

  path ad/
  buffer_path /var/log/td-agent/s3/ad

  time_slice_format %Y%m%d%H
  time_slice_wait 10m
  timezone "Asia/Seoul"
  buffer_chunk_limit 256m
</match>

```
로그서버에서 주의할 점은 udp로 heart bit을 체크하기 때문에 24224번 udp 포트를 방화벽에서 열어줘야 한다.