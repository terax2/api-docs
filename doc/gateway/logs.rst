====================
ixMonitor - Logs API
====================


API List
========

+------------------------------------------------------------+-------------------------------------------------------+
|Endpoint                                                    |Description                                            |
+============================================================+=======================================================+
|:ref:`GET /api/logs/api-key/loglist <get_logs_loglist>`     |<api-key>로 등록된 호스트들의 로그대상 정보 얻기       |
+------------------------------------------------------------+-------------------------------------------------------+
|:ref:`GET /api/logs/api-key/logs/logs <get_logs_logs>`      |<api-key/<logs> 로 등록된 호스트들의 로그 얻기         |
+------------------------------------------------------------+-------------------------------------------------------+
|:ref:`GET /api/logs/api-key/logs/aggr <get_logs_aggr>`      |<api-key/<logs>/<aggr> 로 등록된 호스트들의 로그 집계  |
+------------------------------------------------------------+-------------------------------------------------------+
|:ref:`GET /api/logs/api-key/alerts <get_logs_alerts>`       |<api-key> 로그에 설정된 alert 정보 얻기                |
+------------------------------------------------------------+-------------------------------------------------------+
|:ref:`POST /api/logs/api-key/alerts <post_logs_alerts>`     |<api-key> 로그에 새로운 alert 정보 추가 및 변경하기    |
+------------------------------------------------------------+-------------------------------------------------------+
|:ref:`DELETE /api/logs/api-key/alerts <delete_logs_alerts>` |<api-key> 로그에 기존 alert 정보 삭제하기              |
+------------------------------------------------------------+-------------------------------------------------------+


API Contents
============

.. _get_logs_loglist:

.. http:get:: /api/logs/api-key/loglist

   * <api-key>로 등록된 호스트들의 로그대상 정보 얻기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/logs/7E717E82ED7FB134/loglist?hid=BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "loglist": {
          "kde-r1-dev": [
            {
              "agent_msg": "Log Daemon User ALL Closed",
              "agent_status": "Online",
              "appname": "kinx-agent",
              "filename": "/var/log/kinx-agent/kinx-agent.log",
              "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
              "last_upt": "2020-06-19T16:47:40",
              "regi_dt": "2020-03-02T14:48:54",
              "status": "Normal"
            },
            {
              "agent_msg": "Log Daemon User ALL Closed",
              "agent_status": "Online",
              "appname": "syslog",
              "filename": "syslog",
              "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
              "last_upt": "2020-06-19T16:47:40",
              "regi_dt": "2020-03-06T13:48:47",
              "status": "Normal"
            }
          ]
        }
      }

   * **appname**      로그 대상이 되는 어플리케이션 명
   * **filename**     로그 대상이 되는 어플리케이션에서 발생되는 로그파일
   * **agent_status** 현재 로그 에이전트 접속 상태
   * **last_upt**     마지막 로그 업데이트 일시
   * **regi_dt**      최초로 등록한 로그모니터링 일시
   * **status**       현재 로그에서 발생되는 로그알람 상태


   :queryparam string hid: * **(선택)** host-id
      * 미입력시 default는 ``None``. (api-key에 등록된 서버 전체 출력)
   :queryparam string status: * **(선택)** 등록된 서버들의 status 값 입력
      * (Online/Offline/ALL) 중 택1
      * 미입력시 default는 ``Online``.


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _get_logs_logs:

.. http:get:: /api/logs/api-key/logs/logs

   * <api-key/<logs> 로 등록된 호스트들의 로그 얻기
   * **<logs>**  [syslog | applog] 택1

   **요청 예**:

   .. sourcecode:: http

      GET /api/logs/7E717E82ED7FB134/syslog/logs?start=2020-06-17T13:00:00+09:00&end=2020-06-17T13:29:29+09:00  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "data": {
          "logs": {
            "2020-06-17T13:00:01.313628928+09:00": {
               "appname": "CRON",
               "facility": "10",
               "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
               "hostname": "kde-r1-dev",
               "message": "pam_unix(cron:session): session opened for user root by (uid=0)",
               "pid": "19329",
               "raddr": "1.201.160.22",
               "severity": "info"
            },
            "2020-06-17T13:01:01.967169024+09:00": {
               "appname": "CRON",
               "facility": "10",
               "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
               "hostname": "kde-r1-dev",
               "message": "pam_unix(cron:session): session opened for user root by (uid=0)",
               "pid": "19391",
               "raddr": "1.201.160.22",
               "severity": "info"
            },
            "2020-06-17T13:01:01.979931136+09:00": {
               "appname": "CRON",
               "facility": "9",
               "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
               "hostname": "kde-r1-dev",
               "message": "(root) CMD (/ixMonitor/Common-Receiver/src/influxDB_deleter.py >> /ixMonitor/Common-Receiver/src/influxDB_deleter.log)",
               "pid": "19392",
               "raddr": "1.201.160.22",
               "severity": "info"
            },
            "2020-06-17T13:03:01.382467072+09:00": {
               "appname": "CRON",
               "facility": "10",
               "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
               "hostname": "kde-r1-dev",
               "message": "pam_unix(cron:session): session opened for user root by (uid=0)",
               "pid": "19501",
               "raddr": "1.201.160.22",
               "severity": "info"
            },
            "2020-06-17T13:04:01.246466048+09:00": {
               "appname": "CRON",
               "facility": "9",
               "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
               "hostname": "kde-r1-dev",
               "message": "(root) CMD (/ixMonitor/Common-Receiver/src/influxDB_deleter.py >> /ixMonitor/Common-Receiver/src/influxDB_deleter.log)",
               "pid": "19557",
               "raddr": "1.201.160.22",
               "severity": "info"
            },
            "2020-06-17T13:04:07.794183936+09:00": {
               "appname": "CRON",
               "facility": "10",
               "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
               "hostname": "kde-r1-dev",
               "message": "pam_unix(cron:session): session closed for user root",
               "pid": "19556",
               "raddr": "1.201.160.22",
               "severity": "info"
            }
          },
          "page": "1/2",
          "tags": {
            "akey": "7E717E82ED7FB134"
          },
          "total": 33
        }
      }


   * **hostname** 호스트 네임
   * **appname**  로그 발생 프로그램 명
   * **severity** 로그 발생 등급
   * **pid**      프로그램 ID
   * **raddr**    원격 전송 IP
   * **message**  발생된 메세지


   :queryparam string start: * **(필수)** 가져올 데이터 시작 시간 
      * ``YYYY-MM-DDThh:mm:ss+09:00`` iso8601형식
   :queryparam string end: * **(선택)** 가져올 데이터 끝 시간
      * ``YYYY-MM-DDThh:mm:ss+09:00`` iso8601형식
      * 미입력시 default는 ``0``. (현재시간)
   :queryparam string hid: * **(선택)** host-id
      * 미입력시 default는 ``None``. (api-key에 등록된 서버 전체 출력)
   :queryparam int pid: * **(선택)** 프로그램 ID
      * 미입력시 default는 ``0``.
   :queryparam string hostname: * **(선택)** 서버 hostname
      * 미입력시 default는 ``None``.
   :queryparam string appname: * **(선택)** 로그발생 프로그램 명
      * 미입력시 default는 ``None``.
   :queryparam string severity: * **(선택)** 로그 발생 등급
      * (emerg/alert/crit/err/warn/notice/info/debug) 중 택1
      * 미입력시 default는 ``debug``.
   :queryparam int count: * **(선택)** 페이지당 출력 갯수
      * 미입력시 default는 ``20``.
   :queryparam int page: * **(선택)** 페이지중 현재페이지 (1/3)
      * 미입력시 default는 ``1``.
   :queryparam string order: * **(선택)** 시간순서에 따른 정렬
      * (asc/desc) 중 택1
      * 미입력시 default는 ``asc``.


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류







.. _get_logs_aggr:

.. http:get:: /api/logs/api-key/logs/aggr

   * <api-key/<logs>/<aggr> 로 등록된 호스트들의 로그 집계
   * **<logs>**  [syslog | applog] 택1
   * **<aggr>**  [histogram | terms] 택1

   **요청 예**:

   .. sourcecode:: http

      GET /api/logs/7E717E82ED7FB134/syslog/histogram?start=2020-06-22T11:00:00+09:00&end=2020-06-22T11:20:00+09:00  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "data": {
          "histogram": {
            "2020-06-22T11:00:00+09:00": 3,
            "2020-06-22T11:01:00+09:00": 3,
            "2020-06-22T11:02:00+09:00": 3,
            "2020-06-22T11:03:00+09:00": 3,
            "2020-06-22T11:04:00+09:00": 3,
            "2020-06-22T11:05:00+09:00": 6,
            "2020-06-22T11:06:00+09:00": 3,
            "2020-06-22T11:07:00+09:00": 3,
            "2020-06-22T11:08:00+09:00": 3,
            "2020-06-22T11:09:00+09:00": 3,
            "2020-06-22T11:10:00+09:00": 3,
            "2020-06-22T11:11:00+09:00": 3,
            "2020-06-22T11:12:00+09:00": 8,
            "2020-06-22T11:13:00+09:00": 3,
            "2020-06-22T11:14:00+09:00": 3,
            "2020-06-22T11:15:00+09:00": 6,
            "2020-06-22T11:16:00+09:00": 3,
            "2020-06-22T11:17:00+09:00": 12,
            "2020-06-22T11:18:00+09:00": 3,
            "2020-06-22T11:19:00+09:00": 3,
            "2020-06-22T11:20:00+09:00": 0
          },
          "tags": {
            "logs": "syslog"
          },
          "total": 80
        }
      }


   **요청 예**:

   .. sourcecode:: http

      GET /api/logs/7E717E82ED7FB134/syslog/terms?start=2020-06-22T11:00:00+09:00&end=2020-06-22T11:20:00+09:00&tags=appname  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "data": {
          "tags": {
            "logs": "syslog",
            "field": "appname"
          },
          "terms": [
            {
              "appname": "50-motd-news",
              "count": 3,
              "percent": 3.75
            },
            {
              "appname": "CRON",
              "count": 75,
              "percent": 93.75
            },
            {
              "appname": "systemd",
              "count": 2,
              "percent": 2.5
            }
          ],
          "total": 80
        }
      }


   :queryparam string start: * **(필수)** 가져올 데이터 시작 시간 
      * ``YYYY-MM-DDThh:mm:ss+09:00`` iso8601형식
   :queryparam string end: * **(선택)** 가져올 데이터 끝 시간
      * ``YYYY-MM-DDThh:mm:ss+09:00`` iso8601형식
      * 미입력시 default는 ``0``. (현재시간)
   :queryparam string hid: * **(선택)** host-id
      * 미입력시 default는 ``None``. (api-key에 등록된 서버 전체 출력)
   :queryparam string interval: * **(선택)** 프로그램 ID
      * aggr 값이 histogram 일때만 적용됨.
      * (1m/5m/10m/30m/1h/1d) 중 택1
      * 미입력시 default는 ``1m``.
   :queryparam string tags: * **(선택)** 집계 대상 필드 값
      * aggr 값이 terms 일때는 무조건 집계필드가 필요함.
      * syslog 와 applog 필드가 다름.
      * 미입력시 default는 ``None``.


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _get_logs_alerts:

.. http:get:: /api/logs/api-key/alerts

   * <api-key> 로그에 설정된 alert 정보 얻기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/logs/7E717E82ED7FB134/alerts?group_id=1 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "alerts": {
          "APPLOG": [
            {
               "appname": "kinx-agent",
               "detect_count": 3,
               "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
               "hostname": "kde-r1-dev",
               "msg_express": "Metric & Test",
               "send_day_max": 3,
               "send_interval": 180,
               "sender_group": {
                  "id": 1,
                  "name": "기본발송"
               },
               "seq": 2
            },
            {
               "appname": "kinx-agent",
               "detect_count": 10,
               "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
               "hostname": "kde-r1-dev2",
               "msg_express": "Metric & Send",
               "send_day_max": 3,
               "send_interval": 180,
               "sender_group": {
                  "id": 1,
                  "name": "기본발송"
               },
               "seq": 4
            },
            {
               "appname": "kinx-agent",
               "detect_count": 3,
               "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
               "hostname": "test-dev",
               "msg_express": "Metric & Send",
               "send_day_max": 3,
               "send_interval": 180,
               "sender_group": {
                  "id": 1,
                  "name": "기본발송"
               },
               "seq": 5
            }
          ],
          "SYSLOG": [
            {
               "appname": "influxd",
               "detect_count": 10,
               "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
               "hostname": "kde-r1-dev",
               "msg_express": "POST & Next",
               "send_day_max": 3,
               "send_interval": 180,
               "sender_group": {
                  "id": 1,
                  "name": "기본발송"
               },
               "seq": 1,
               "severity": "debug"
            }
          ]
        }
      }


   * **hostname**      호스트 네임
   * **appname**       로그 발생 프로그램 명
   * **severity**      로그 레벨 이상 (debug : debug 이상, warn : warnig 이상)
   * **msg_express**   message 필드에 대해서 regular expression 처리 가능. (and == &, or == | 조건 처리 가능)
   * **detect_count**  모니터링 대상 조건에 감지 횟수 (횟수 만큼 감지되면 알람 발생됨 - 지속적인 위험을 체크하기 위함)
   * **send_interval** 알람전송후 다시 전송될 최소한의 간격을 지정함. (기본값 3분)
   * **send_day_max**  알람 전송 횟수를 하루 최대 횟수 설정. (SMS, Email, Slack 등등)
   * **sender_id**     해당 알람을 전송 대상 목록이 정의된 ID 값
   * **seq**           화면상에서는 보이지 않음.  alert 내용을 수정하거나 삭제할때 반드시 필요 함.  만약에 POST 상태에서 seq 값이 없을 경우에는 추가 등록처리 된다.
   
   :queryparam int group_id: * **(필수)** 호스트 그룹ID
   :queryparam string hid: * **(선택)** host-id
      * 미입력시 default는 ``None``. (api-key에 등록된 서버 전체 출력)

   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _post_logs_alerts:

.. http:post:: /api/logs/api-key/alerts

   * <api-key> 로그에 새로운 alert 정보 추가 및 변경하기

   **요청 예**:

   .. sourcecode:: http

      POST /api/logs/7E717E82ED7FB134/alerts?group_id=1 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      {
        "hosts": ["BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE"]
        "alerts": {
          "APPLOG": [
            {
               "appname": "kinx-agent",
               "detect_count": 3,
               "hostname": "test-dev",
               "msg_express": "Metric & Send",
               "send_day_max": 3,
               "send_interval": 180,
               "sender_id": 1,
               "seq": 5
            }
          ],
          "SYSLOG": [
            {
               "appname": "influxd",
               "detect_count": 10,
               "hostname": "kde-r1-dev",
               "msg_express": "POST & Next",
               "send_day_max": 3,
               "send_interval": 180,
               "sender_id": 1,
               "seq": 1,
               "severity": "debug"
            }
          ]
        }
      }


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }

   :queryparam int group_id: * **(필수)** 호스트 그룹ID

   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _delete_logs_alerts:

.. http:delete:: /api/logs/api-key/alerts

   * <api-key> 로그에 기존 alert 정보 삭제하기

   **요청 예**:

   .. sourcecode:: http

      DELETE /api/logs/7E717E82ED7FB134/alerts?group_id=1 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 삭제정보

      {
        "hosts":["BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE"],
        "alerts": {
          "SYSLOG": [
            {
            "appname": "influxd",
            "detect_count": 5,
            "hostname": "kde-r1-dev",
            "msg_express": "POST & Next",
            "send_day_max": 3,
            "send_interval": 180,
            "sender_id": 1,
            "seq": 1,
            "severity": "debug"
            }
          ]
        }
      }


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }

   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류
