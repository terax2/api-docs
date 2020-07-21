=======================
ixMonitor - Metrics API
=======================


API List
========

+------------------------------------------------------------------+------------------------------------------------------------+
|Endpoint                                                          |Description                                                 |
+==================================================================+============================================================+
|:ref:`GET /api/metrics/api-key/hosts <get_metrics_hosts>`         |<api-key> 값으로 등록된 호스트 정보 얻기                    |
+------------------------------------------------------------------+------------------------------------------------------------+
|:ref:`GET /api/metrics/api-key/alerts <get_metrics_alerts>`       |<api-key> 값으로 등록된 호스트별 Alert 정보                 |
+------------------------------------------------------------------+------------------------------------------------------------+
|:ref:`POST /api/metrics/api-key/alerts <post_metrics_alerts>`     |<api-key> 값으로 등록된 호스트별 Alert 수정,추가            |
+------------------------------------------------------------------+------------------------------------------------------------+
|:ref:`DELETE /api/metrics/api-key/alerts <delete_metrics_alerts>` |<api-key> 값으로 등록된 호스트별 Alert 정보 삭제            |
+------------------------------------------------------------------+------------------------------------------------------------+
|:ref:`GET /api/metrics/hid/list <get_metrics_list>`               |<hid> 값으로 등록된 메트릭명:단위 정보 얻기.                |
+------------------------------------------------------------------+------------------------------------------------------------+
|:ref:`GET /api/metrics/hid/last <get_metrics_last>`               |<hid> 값으로 마지막 값 얻기                                 |
+------------------------------------------------------------------+------------------------------------------------------------+
|:ref:`GET /api/metrics/hid/metric <get_metrics_dps>`              |<hid>/<metric> 수집된 해당 metric 값 얻기                   |
+------------------------------------------------------------------+------------------------------------------------------------+
|:ref:`GET /api/metrics/hid/proc/last <get_metrics_proc_last>`     |<hid> process 별 metric 마지막 값 얻기                      |
+------------------------------------------------------------------+------------------------------------------------------------+
|:ref:`GET /api/metrics/hid/proc/metric <get_metrics_proc_dps>`    |<hid>/proc/<metric> process 별 수집된 해당 metric 값 얻기   |
+------------------------------------------------------------------+------------------------------------------------------------+
|:ref:`GET /api/metrics/hid/alert <get_metrics_alert>`             |<hid> 메트릭에 설정된 alert 정보 얻기                       |
+------------------------------------------------------------------+------------------------------------------------------------+
|:ref:`POST /api/metrics/hid/alert <post_metrics_alert>`           |<hid> 메트릭에 새로운 alert 정보 추가 및 변경하기           |
+------------------------------------------------------------------+------------------------------------------------------------+
|:ref:`DELETE /api/metrics/hid/alert <delete_metrics_alert>`       |<hid> 메트릭에 기존 alert 정보 삭제하기                     |
+------------------------------------------------------------------+------------------------------------------------------------+


API Contents
============

.. _get_metrics_hosts:

.. http:get:: /api/metrics/api-key/hosts

   * <api-key> 값으로 등록된 호스트 정보 얻기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/metrics/7E717E82ED7FB134/hosts?count=20&page=1  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "data": {
          "hosts": [
            {
              "agent": "Online",
              "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
              "hostname": "kde-r1-dev",
              "last_date": "2020-06-23T15:47:00+09:00",
              "last_value": {
                "cpu": 0.9,
                "disk": 17.45,
                "loadavg": 5.5,
                "mem": 63.48,
                "network": {
                  "inbps": 20528,
                  "outbps": 33120
                }
              },
              "os_system": "Linux",
              "status": "Normal"
            },
            {
              "agent": "Online",
              "hid": "CCA11FCF-87FC-4F0B-A1C0-E37C586CE6B7",
              "hostname": "test-dev",
              "last_date": "2020-06-23T15:46:39+09:00",
              "last_value": {
                "cpu": 0,
                "disk": 9.4,
                "loadavg": 0,
                "mem": 2.95,
                "network": {
                  "inbps": 184,
                  "outbps": 1176
                }
              },
              "os_system": "Linux",
              "status": "Normal"
            },
            {
              "agent": "Online",
              "hid": "CB7A2A6E-102A-414C-8DBB-80AFCDC8C4FD",
              "hostname": "kde-r1-dev2",
              "last_date": "2020-06-23T15:46:31+09:00",
              "last_value": {
                "cpu": 0.4,
                "disk": 2.2,
                "loadavg": 0,
                "mem": 7.06,
                "network": {
                  "inbps": 23040,
                  "outbps": 7456
                }
              },
              "os_system": "Linux",
              "status": "Normal"
            }
          ],
          "page": "1/1",
          "total": 3
        }
      }

   * **last_date**  에이전트에서 마지막으로 수집된 메트릭 시간
   * **last_value** 에이전트에서 마지막으로 수집된 메트릭 5가지 값 (CPU:%, disk:%, loadavg:%, mem:%, network:bps)

   :queryparam int count: * **(선택)** 페이지당 출력 갯수
      * 미입력시 default는 ``20``.
   :queryparam int page: * **(선택)** 페이지중 현재페이지 (1/3)
      * 미입력시 default는 ``1``.


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류






.. _get_metrics_alerts:

.. http:get:: /api/metrics/api-key/alerts

   * <api-key> 값으로 등록된 호스트별 Alert 정보.

   **요청 예**:

   .. sourcecode:: http

      GET /api/metrics/7E717E82ED7FB134/alerts?group_id=1  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "alerts": {
          "001.kde-r1-dev": {
            "CPU": [
              {
                "detect_count": 3,
                "device": "cpu_t",
                "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
                "high": 30.0,
                "metric": "idle",
                "middle": 42.0,
                "reverse": "Y",
                "send_day_max": 3,
                "send_interval": 180,
                "sender_group": {
                  "id": 1,
                  "name": "sms 발송"
                },
                "seq_id": 1
              }
            ],
            "DISK": [
              {
                "detect_count": 3,
                "device": "vdb1",
                "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
                "high": 80.0,
                "metric": "percent",
                "middle": 70.0,
                "reverse": "N",
                "send_day_max": 3,
                "send_interval": 180,
                "sender_group": {
                  "id": 1,
                  "name": "sms 발송"
                },
                "seq_id": 2
              }
            ],
            "MEM": [
              {
                "detect_count": 3,
                "device": "ALL",
                "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
                "high": 70.0,
                "metric": "percent",
                "middle": 50.0,
                "reverse": "N",
                "send_day_max": 3,
                "send_interval": 180,
                "sender_group": {
                  "id": 1,
                  "name": "sms 발송"
                },
                "seq_id": 4
              }
            ],
            "NETWORK": [
              {
                "detect_count": 3,
                "device": "ens3",
                "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
                "high": 1000000.0,
                "metric": "inbps",
                "middle": 800000.0,
                "reverse": "N",
                "send_day_max": 3,
                "send_interval": 180,
                "sender_group": {
                  "id": 1,
                  "name": "sms 발송"
                },
                "seq_id": 5
              }
            ],
            "OFF": [
              {
                "detect_count": 3,
                "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
                "sender_group": {
                  "id": 1,
                  "name": "sms 발송"
                },
                "seq_id": 6
              }
            ],
            "SYSTEM": [
              {
                "detect_count": 3,
                "device": "ALL",
                "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
                "high": 30.0,
                "metric": "load1",
                "middle": 10.0,
                "reverse": "N",
                "send_day_max": 3,
                "send_interval": 180,
                "sender_group": {
                  "id": 1,
                  "name": "sms 발송"
                },
                "seq_id": 7
              }
            ]
          }
        }
      }


   * **hostname**     호스트네임별
     .. **hid**           호스트 ID
     .. **category**      항목 구분 ('CPU', 'DISK', 'DISKIO', 'MEM', 'NETWORK', 'SYSTEM', 'OFF')
     .. **device**        디바이스
     .. **metric**        디바이스의 상세 항목
     .. **reverse**       'Y': 수치가 낮을수록 위험, 'N' : 수치가 높을수록 위험. (일반적으로 'N' 값이 기본값임)
     .. **high**          Alert - 경고 수치 값
     .. **middle**        Warning - 경고 수치 값
     .. **detect_count**  연속 감지 횟수
     .. **send_interval** 알람 발송 간격
     .. **send_day_max**  하루 최대 발송 횟수
     .. **sender_group**  알람발생시 전송할 발송 그룹
     .. **seq_id**        해당 Alert 시퀀스번호


   :queryparam int group_id: * **(필수)** 해당 호스트그룹 ID
   :queryparam string hid: * **(선택)** 지정 호스트 ID
      * 미입력시 default는 ``None : 그룹전체호스트``.


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류






.. _post_metrics_alerts:

.. http:post:: /api/metrics/api-key/alerts

   * <api-key> 값으로 등록된 호스트별 Alert 수정, 추가.

   **요청 예**:

   .. sourcecode:: http

      POST /api/metrics/7E717E82ED7FB134/alerts?group_id=1  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      {
        "hosts":["BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE"],
        "metrics": {
          "CPU": [
            {
              "detect_count": 3,
              "device": "cpu_t",
              "high": 30.0,
              "metric": "idle",
              "middle": 42.0,
              "reverse": "Y",
              "send_day_max": 3,
              "send_interval": 180,
              "sender_id": 1
            }
          ]
        }
      }

      * **hosts**     적용될 호스트ID 목록
      * **metrics**   수정 및 삭제 Alert 정보
        .. **category**      항목 구분 ('CPU', 'DISK', 'DISKIO', 'MEM', 'NETWORK', 'SYSTEM', 'OFF')
        .. **device**        디바이스
        .. **metric**        디바이스의 상세 항목
        .. **reverse**       'Y': 수치가 낮을수록 위험, 'N' : 수치가 높을수록 위험. (일반적으로 'N' 값이 기본값임)
        .. **high**          Alert - 경고 수치 값
        .. **middle**        Warning - 경고 수치 값
        .. **detect_count**  연속 감지 횟수
        .. **send_interval** 알람 발송 간격
        .. **send_day_max**  하루 최대 발송 횟수
        .. **sender_id**     알람 발송 그룹에서 선택된 발송그룹ID 값


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }


   :queryparam int group_id: * **(필수)** 해당 호스트그룹 ID
   :queryparam string hid: * **(선택)** 지정 호스트 ID
      * 미입력시 default는 ``None : 그룹전체호스트``.


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류






.. _delete_metrics_alerts:

.. http:delete:: /api/metrics/api-key/alerts

   * <api-key> 값으로 등록된 호스트별 Alert 정보 삭제.

   **요청 예**:

   .. sourcecode:: http

      DELETE /api/metrics/7E717E82ED7FB134/alerts?group_id=1  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      {
        "hosts":["BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE"],
        "metrics": {
          "CPU": [
            {
              "seq_id": 1
            }
          ]
        }
      }

      * **hosts**     삭제될 대상 호스트ID 목록
      * **metrics**   수정 및 삭제 Alert 정보
        .. **category**      항목 구분 ('CPU', 'DISK', 'DISKIO', 'MEM', 'NETWORK', 'SYSTEM', 'OFF')
        .. **seq_id**        Alert seq-id


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }


   :queryparam int group_id: * **(필수)** 해당 호스트그룹 ID
   :queryparam string hid: * **(선택)** 지정 호스트 ID
      * 미입력시 default는 ``None : 그룹전체호스트``.


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류






.. _get_metrics_list:

.. http:get:: /api/metrics/hid/list

   * <hid> 값으로 등록된 메트릭명:단위 정보 얻기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/metrics/BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE/list?metric=cpu  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "metrics": {
          "CPU": {
            "device": [
              "cpu_t",
              "cpu_0",
              "cpu_1",
              "cpu_2",
              "cpu_3"
            ],
            "metric": {
              "guest": "%",
              "guest_nice": "%",
              "idle": "%",
              "iowait": "%",
              "irq": "%",
              "nice": "%",
              "softirq": "%",
              "steal": "%",
              "system": "%",
              "user": "%"
            }
          }
        }
      }

   * **device** 해당서버에서 사용되는 디바이스
   * **metric** 해당 디바이스에서 사용되는 메트릭과 메트릭의 단위 (메트릭명:단위)



   :queryparam string metric: * **(선택)** 메트릭 선택
      * (cpu/mem/disk/diskio/network/system/port/custom/swap/proc_cpu/proc_mem/proc_diskio/syslog/applog) 중 택1
      * 미입력시 default는 ``None``. (전체출력)



   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _get_metrics_last:

.. http:get:: /api/metrics/hid/last

   * <hid> 값으로 마지막 값 얻기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/metrics/BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE/last  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "last": {
          "cpu": [
            {
              "dev": "cpu_0",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "guest": 0,
                  "guest_nice": 0,
                  "idle": 99.5,
                  "iowait": 0,
                  "irq": 0,
                  "nice": 0,
                  "percent": 0.5,
                  "softirq": 0,
                  "steal": 0,
                  "system": 0.1,
                  "user": 0.4
                }
              }
            },
            {
              "dev": "cpu_1",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "guest": 0,
                  "guest_nice": 0,
                  "idle": 99,
                  "iowait": 0.2,
                  "irq": 0,
                  "nice": 0,
                  "percent": 0.8,
                  "softirq": 0,
                  "steal": 0,
                  "system": 0.3,
                  "user": 0.5
                }
              }
            },
            {
              "dev": "cpu_2",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "guest": 0,
                  "guest_nice": 0,
                  "idle": 98.7,
                  "iowait": 0,
                  "irq": 0,
                  "nice": 0,
                  "percent": 1.2,
                  "softirq": 0,
                  "steal": 0,
                  "system": 0.6,
                  "user": 0.6
                }
              }
            },
            {
              "dev": "cpu_3",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "guest": 0,
                  "guest_nice": 0,
                  "idle": 98.9,
                  "iowait": 0.3,
                  "irq": 0,
                  "nice": 0,
                  "percent": 0.8,
                  "softirq": 0,
                  "steal": 0,
                  "system": 0.1,
                  "user": 0.7
                }
              }
            },
            {
              "dev": "cpu_t",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "guest": 0,
                  "guest_nice": 0,
                  "idle": 99,
                  "iowait": 0.1,
                  "irq": 0,
                  "nice": 0,
                  "percent": 0.8,
                  "softirq": 0,
                  "steal": 0,
                  "system": 0.3,
                  "user": 0.5
                }
              }
            }
          ],
          "custom": [
            {
              "dev": "cmd.ls",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "result": "28"
                }
              }
            },
            {
              "dev": "cmd.test",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "result": "28"
                }
              }
            },
            {
              "dev": "host.ls",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "result": "28"
                }
              }
            },
            {
              "dev": "python.test",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "result": "28"
                }
              }
            }
          ],
          "disk": [
            {
              "dev": "vda1",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "free": 41173176320,
                  "fstype": "ext4",
                  "mode": "rw",
                  "mountpoint": "/",
                  "percent": 20.8,
                  "total": 51976970240,
                  "used": 10787016704
                }
              }
            },
            {
              "dev": "vdb1",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "free": 42978942976,
                  "fstype": "ext4",
                  "mode": "rw",
                  "mountpoint": "/DBdata",
                  "percent": 14.1,
                  "total": 52709421056,
                  "used": 7029399552
                }
              }
            }
          ],
          "diskio": [
            {
              "dev": "vda",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "disk_iops": 1,
                  "io_time": 4,
                  "read_bytes": 0,
                  "read_count": 0,
                  "read_mergeds": 0,
                  "read_sectors": 0,
                  "read_time": 0,
                  "write_bytes": 561152,
                  "write_count": 41,
                  "write_mergeds": 91,
                  "write_sectors": 1096,
                  "write_time": 4
                }
              }
            },
            {
              "dev": "vda1",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "disk_iops": 1,
                  "io_time": 4,
                  "read_bytes": 0,
                  "read_count": 0,
                  "read_mergeds": 0,
                  "read_sectors": 0,
                  "read_time": 0,
                  "write_bytes": 561152,
                  "write_count": 41,
                  "write_mergeds": 91,
                  "write_sectors": 1096,
                  "write_time": 4
                }
              }
            },
            {
              "dev": "vdb",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "disk_iops": 13,
                  "io_time": 192,
                  "read_bytes": 0,
                  "read_count": 0,
                  "read_mergeds": 0,
                  "read_sectors": 0,
                  "read_time": 0,
                  "write_bytes": 4882432,
                  "write_count": 394,
                  "write_mergeds": 165,
                  "write_sectors": 9536,
                  "write_time": 208
                }
              }
            },
            {
              "dev": "vdb1",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "disk_iops": 12,
                  "io_time": 192,
                  "read_bytes": 0,
                  "read_count": 0,
                  "read_mergeds": 0,
                  "read_sectors": 0,
                  "read_time": 0,
                  "write_bytes": 4882432,
                  "write_count": 381,
                  "write_mergeds": 165,
                  "write_sectors": 9536,
                  "write_time": 208
                }
              }
            }
          ],
          "mem": [
            {
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "active": 6577909760,
                  "available": 2753425408,
                  "buffers": 290369536,
                  "cached": 2497429504,
                  "free": 366305280,
                  "inactive": 990486528,
                  "percent": 62.32,
                  "shared": 84869120,
                  "slab": 356667392,
                  "swap_free": 0,
                  "swap_percent": 0,
                  "swap_sin": 0,
                  "swap_sout": 0,
                  "swap_total": 0,
                  "swap_used": 0,
                  "total": 8371113984,
                  "used": 5217009664
                }
              }
            }
          ],
          "network": [
            {
              "dev": "ens3",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "dropin": 0,
                  "dropout": 0,
                  "errin": 0,
                  "errout": 0,
                  "inbps": 20488,
                  "inpps": 100,
                  "outbps": 32872,
                  "outpps": 112
                }
              }
            },
            {
              "dev": "lo",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "dropin": 0,
                  "dropout": 0,
                  "errin": 0,
                  "errout": 0,
                  "inbps": 124696,
                  "inpps": 811,
                  "outbps": 124696,
                  "outpps": 811
                }
              }
            }
          ],
          "port": [
            {
              "dev": "mysql",
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "status": "OK"
                }
              },
              "port": "3306"
            }
          ],
          "system": [
            {
              "dps": {
                "2020-06-23T16:02:00+09:00": {
                  "bootime": "2019-08-20T11:20:37+09:00",
                  "conntrack_cnt": 0,
                  "conntrack_max": 262144,
                  "load1": 2.75,
                  "load15": 5.75,
                  "load5": 4.5,
                  "n_cpu": 4,
                  "n_user": 3,
                  "swappiness": 60,
                  "uptime": 26628083.3
                }
              }
            }
          ]
        }
      }


   :queryparam string metric: * **(선택)** 메트릭 항목 선택 가능
      * (cpu/mem/disk/diskio/network/system/port/custom/swap) 중 택1
      * 미입력시 default는 ``None``. (전체출력)


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류




.. _get_metrics_dps:

.. http:get:: /api/metrics/hid/metric

   * <hid>/<metric> 수집된 해당 metric 값 얻기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/metrics/BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE/mem?start=2020-06-22T10:00:00+09:00&end=2020-06-22T12:00:00+09:00  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "data": {
          "dps": {
            "2020-06-22T10:00:31+09:00": {
              "active": 1531650048,
              "available": 7508078592,
              "buffers": 321314816,
              "cached": 1971515392,
              "free": 5540085760,
              "inactive": 1013780480,
              "percent": 6.43,
              "shared": 9048064,
              "slab": 240762880,
              "total": 8371113984,
              "used": 538198016
            },
            "2020-06-22T10:01:31+09:00": {
              "active": 1531928576,
              "available": 7507222528,
              "buffers": 321314816,
              "cached": 1971703808,
              "free": 5539041280,
              "inactive": 1013878784,
              "percent": 6.44,
              "shared": 9048064,
              "slab": 240766976,
              "total": 8371113984,
              "used": 539054080
            },
            "2020-06-22T10:02:31+09:00": {
              "active": 1531940864,
              "available": 7507062784,
              "buffers": 321314816,
              "cached": 1971867648,
              "free": 5538717696,
              "inactive": 1013972992,
              "percent": 6.44,
              "shared": 9048064,
              "slab": 240762880,
              "total": 8371113984,
              "used": 539213824
            },
            "2020-06-22T10:03:31+09:00": {
              "active": 1531023360,
              "available": 7508201472,
              "buffers": 321314816,
              "cached": 1972035584,
              "free": 5539688448,
              "inactive": 1014063104,
              "percent": 6.43,
              "shared": 9048064,
              "slab": 240820224,
              "total": 8371113984,
              "used": 538075136
            },
            "2020-06-22T10:04:31+09:00": {
              "active": 1531109376,
              "available": 7508123648,
              "buffers": 321314816,
              "cached": 1972199424,
              "free": 5539446784,
              "inactive": 1014165504,
              "percent": 6.43,
              "shared": 9048064,
              "slab": 240807936,
              "total": 8371113984,
              "used": 538152960
            },
            "2020-06-22T10:05:31+09:00": {
              "active": 1541066752,
              "available": 7500521472,
              "buffers": 321314816,
              "cached": 1972531200,
              "free": 5531512832,
              "inactive": 1014272000,
              "percent": 6.52,
              "shared": 9048064,
              "slab": 240758784,
              "total": 8371113984,
              "used": 545755136
            },
            "2020-06-22T10:06:31+09:00": {
              "active": 1544724480,
              "available": 7495954432,
              "buffers": 321314816,
              "cached": 1972760576,
              "free": 5526716416,
              "inactive": 1014370304,
              "percent": 6.57,
              "shared": 9048064,
              "slab": 240758784,
              "total": 8371113984,
              "used": 550322176
            },
            "2020-06-22T10:07:31+09:00": {
              "active": 1544675328,
              "available": 7495901184,
              "buffers": 321314816,
              "cached": 1972928512,
              "free": 5526495232,
              "inactive": 1014456320,
              "percent": 6.57,
              "shared": 9048064,
              "slab": 240758784,
              "total": 8371113984,
              "used": 550375424
            },
            "2020-06-22T10:08:31+09:00": {
              "active": 1543090176,
              "available": 7494909952,
              "buffers": 321314816,
              "cached": 1973096448,
              "free": 5525336064,
              "inactive": 1014550528,
              "percent": 6.59,
              "shared": 9048064,
              "slab": 240758784,
              "total": 8371113984,
              "used": 551366656
            },
            "2020-06-22T10:09:31+09:00": {
              "active": 1545179136,
              "available": 7495331840,
              "buffers": 321314816,
              "cached": 1973260288,
              "free": 5525594112,
              "inactive": 1014644736,
              "percent": 6.58,
              "shared": 9048064,
              "slab": 240758784,
              "total": 8371113984,
              "used": 550944768
            }
          },
          "tags": {
            "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
            "metric": "mem"
          },
          "total": 10
        }
      }


   :queryparam string start: * **(필수)** 가져올 데이터 시작 시간 
      * ``YYYY-MM-DDThh:mm:ss+09:00`` iso8601형식
   :queryparam string end: * **(선택)** 가져올 데이터 끝 시간
      * ``YYYY-MM-DDThh:mm:ss+09:00`` iso8601형식
      * 미입력시 default는 ``0``. (현재시간)
   :queryparam string <metric>: * **(필수)** 가져올 메트릭 선택 가능
      * (cpu/mem/disk/diskio/network/system/port/custom/swap) 중 택1
   :queryparam string aggr: * **(선택)** 메트릭 집계 데이타
      * (5m/1h/1d) 중 택1 ``5m``: 5분집계, ``1h``: 1시간집계, ``1d``: 1일집계
      * 미입력시 default는 ``None``.
   :queryparam string device: * **(선택)** metric 별로 선택 가능한 device 값 선택
      * 미입력시 default는 ``all``. (모든 device 출력)
   :queryparam int port: * **(선택)** 메트릭 항목이 ``port`` 일 경우 포트 번호 지정
      * 미입력시 default는 ``0``.


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _get_metrics_proc_last:

.. http:get:: /api/metrics/hid/proc/last

   * <hid> process 별 metric 마지막 값 얻기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/metrics/BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE/proc/last  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "proc_last": {
          "dps": [
            {
              "name": "python",
              "pid": "11414",
              "proc_cpu": 0.8,
              "proc_iops": 184,
              "proc_mem": 73998336
            },
            {
              "name": "alert_manager",
              "pid": "16821",
              "proc_cpu": 0.43,
              "proc_iops": 1,
              "proc_mem": 548319232
            },
            {
              "name": "influxd",
              "pid": "23251",
              "proc_cpu": 0.43,
              "proc_iops": 7,
              "proc_mem": 1468104704
            },
            {
              "name": "metric_recv",
              "pid": "23377",
              "proc_cpu": 0.43,
              "proc_iops": 1,
              "proc_mem": 76963840
            },
            {
              "name": "java",
              "pid": "27096",
              "proc_cpu": 0.27,
              "proc_iops": 1,
              "proc_mem": 1527070720
            },
            {
              "name": "mysqld",
              "pid": "18870",
              "proc_cpu": 0.17,
              "proc_iops": 3,
              "proc_mem": 417677312
            },
            {
              "name": "python",
              "pid": "30206",
              "proc_cpu": 0.17,
              "proc_iops": 0,
              "proc_mem": 20586496
            },
            {
              "name": "redis-server",
              "pid": "5172",
              "proc_cpu": 0.13,
              "proc_iops": 26,
              "proc_mem": 11694080
            },
            {
              "name": "python",
              "pid": "30203",
              "proc_cpu": 0.13,
              "proc_iops": 0,
              "proc_mem": 19734528
            },
            {
              "name": "gunicorn:_worker_[common-gateway]",
              "pid": "6121",
              "proc_cpu": 0.1,
              "proc_iops": 0,
              "proc_mem": 66555904
            },
            {
              "name": "gunicorn:_worker_[common-gateway]",
              "pid": "30005",
              "proc_cpu": 0.1,
              "proc_iops": 0,
              "proc_mem": 66551808
            },
            {
              "name": "python",
              "pid": "30205",
              "proc_cpu": 0.1,
              "proc_iops": 0,
              "proc_mem": 19787776
            },
            {
              "name": "gunicorn:_worker_[common-gateway]",
              "pid": "2981",
              "proc_cpu": 0.07,
              "proc_iops": 0,
              "proc_mem": 67420160
            },
            {
              "name": "gunicorn:_worker_[common-gateway]",
              "pid": "11141",
              "proc_cpu": 0.07,
              "proc_iops": 0,
              "proc_mem": 66772992
            },
            {
              "name": "influxdb-relay",
              "pid": "23318",
              "proc_cpu": 0.07,
              "proc_iops": 12,
              "proc_mem": 8937472
            },
            {
              "name": "gunicorn:_worker_[Web-gateway]",
              "pid": "32550",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 68468736
            },
            {
              "name": "gunicorn:_master_[common-gateway]",
              "pid": "11136",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 23568384
            },
            {
              "name": "supervisord",
              "pid": "11134",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 17911808
            },
            {
              "name": "python",
              "pid": "12584",
              "proc_cpu": 0.03,
              "proc_iops": 1,
              "proc_mem": 56840192
            },
            {
              "name": "gunicorn:_worker_[Web-gateway]",
              "pid": "32539",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 68190208
            },
            {
              "name": "supervisord",
              "pid": "32527",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 19972096
            },
            {
              "name": "gunicorn:_worker_[Web-gateway]",
              "pid": "32538",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 61923328
            },
            {
              "name": "gunicorn:_worker_[common-gateway]",
              "pid": "14604",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 66793472
            },
            {
              "name": "gunicorn:_worker_[common-gateway]",
              "pid": "11144",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 66093056
            },
            {
              "name": "gunicorn:_worker_[common-gateway]",
              "pid": "11143",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 67022848
            },
            {
              "name": "python",
              "pid": "30207",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 19521536
            },
            {
              "name": "jbd2/vda1-8",
              "pid": "299",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 0
            },
            {
              "name": "gunicorn:_master_[Web-gateway]",
              "pid": "32531",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 25378816
            },
            {
              "name": "gunicorn:_worker_[Web-gateway]",
              "pid": "32536",
              "proc_cpu": 0.03,
              "proc_iops": 0,
              "proc_mem": 61956096
            },
            {
              "name": "gunicorn:_worker_[Web-gateway]",
              "pid": "32542",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 68182016
            },
            {
              "name": "gunicorn:_worker_[Web-gateway]",
              "pid": "32551",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 68206592
            },
            {
              "name": "alert_manager",
              "pid": "16820",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 531529728
            },
            {
              "name": "python",
              "pid": "30210",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 19386368
            },
            {
              "name": "python",
              "pid": "12583",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 56664064
            },
            {
              "name": "python",
              "pid": "12580",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 55336960
            },
            {
              "name": "jbd2/vdb1-8",
              "pid": "26348",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 0
            },
            {
              "name": "gunicorn:_worker_[common-gateway]",
              "pid": "15643",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 65527808
            },
            {
              "name": "systemd",
              "pid": "1",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 5439488
            },
            {
              "name": "kworker/u8:0",
              "pid": "29155",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 0
            },
            {
              "name": "gunicorn:_worker_[Web-gateway]",
              "pid": "32544",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 68624384
            },
            {
              "name": "accounts-daemon",
              "pid": "1037",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 3387392
            },
            {
              "name": "systemd-logind",
              "pid": "1035",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 4485120
            },
            {
              "name": "gunicorn:_worker_[Web-gateway]",
              "pid": "32549",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 68169728
            },
            {
              "name": "python",
              "pid": "30199",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 18317312
            },
            {
              "name": "gunicorn:_worker_[common-gateway]",
              "pid": "30862",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 65773568
            },
            {
              "name": "gunicorn:_worker_[Web-gateway]",
              "pid": "32541",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 68239360
            },
            {
              "name": "kworker/u8:1",
              "pid": "29898",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 0
            },
            {
              "name": "python",
              "pid": "30208",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 20705280
            },
            {
              "name": "python",
              "pid": "30204",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 20561920
            },
            {
              "name": "python",
              "pid": "30211",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 20561920
            },
            {
              "name": "python",
              "pid": "30202",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 20578304
            },
            {
              "name": "systemd-journald",
              "pid": "375",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 10035200
            },
            {
              "name": "python",
              "pid": "30209",
              "proc_cpu": 0,
              "proc_iops": 0,
              "proc_mem": 20344832
            }
          ],
          "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
          "time": "2020-06-23T16:58:00+09:00"
        }
      }



   :queryparam string sort: * **(선택)** 프로세스 정렬기준 선택
      * (proc_cpu/proc_mem/proc_diskio) 중 택1
      * 미입력시 default는 ``proc_cpu``.


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류




.. _get_metrics_proc_dps:

.. http:get:: /api/metrics/hid/proc/metric

   * <hid>/proc/<metric> process 별 수집된 해당 metric 값 얻기

   **요청 예**:

   .. sourcecode:: http

      GET /api/metrics/BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE/proc/proc_cpu?start=2020-06-12T15:00:00+09:00&end=2020-06-12T15:10:00+09:00&pid=23251  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "data": {
          "total": 21,
          "dps": {
            "2020-06-22T15:08:00+09:00": {
                "iowait": 0,
                "percent": 0.4,
                "system": 0.02,
                "child_user": 0,
                "user": 0.1,
                "child_sys": 0
            },
            "2020-06-22T15:07:00+09:00": {
                "iowait": 0,
                "percent": 2.27,
                "system": 0.02,
                "child_user": 0,
                "user": 0.66,
                "child_sys": 0
            },
            "2020-06-22T15:02:00+09:00": {
                "iowait": 0,
                "percent": 0.4,
                "system": 0.01,
                "child_user": 0,
                "user": 0.11,
                "child_sys": 0
            },
            "2020-06-22T15:02:30+09:00": {
                "iowait": 0,
                "percent": 38.07,
                "system": 0.14,
                "child_user": 0,
                "user": 11.28,
                "child_sys": 0
            },
            "2020-06-22T15:09:00+09:00": {
                "iowait": 0,
                "percent": 0.43,
                "system": 0.01,
                "child_user": 0,
                "user": 0.12,
                "child_sys": 0
            },
            "2020-06-22T15:00:00+09:00": {
                "iowait": 0,
                "percent": 0.37,
                "system": 0.03,
                "child_user": 0,
                "user": 0.08,
                "child_sys": 0
            },
            "2020-06-22T15:08:30+09:00": {
                "iowait": 0,
                "percent": 37.13,
                "system": 0.13,
                "child_user": 0,
                "user": 11.01,
                "child_sys": 0
            },
            "2020-06-22T15:03:30+09:00": {
                "iowait": 0,
                "percent": 37.8,
                "system": 0.14,
                "child_user": 0,
                "user": 11.2,
                "child_sys": 0
            },
            "2020-06-22T15:01:30+09:00": {
                "iowait": 0,
                "percent": 37.37,
                "system": 0.12,
                "child_user": 0,
                "user": 11.09,
                "child_sys": 0
            },
            "2020-06-22T15:07:30+09:00": {
                "iowait": 0,
                "percent": 35.5,
                "system": 0.12,
                "child_user": 0,
                "user": 10.53,
                "child_sys": 0
            },
            "2020-06-22T15:01:00+09:00": {
                "iowait": 0,
                "percent": 0.47,
                "system": 0,
                "child_user": 0,
                "user": 0.14,
                "child_sys": 0
            },
            "2020-06-22T15:04:30+09:00": {
                "iowait": 0,
                "percent": 38.47,
                "system": 0.12,
                "child_user": 0,
                "user": 11.42,
                "child_sys": 0
            },
            "2020-06-22T15:10:00+09:00": {
                "iowait": 0,
                "percent": 0.4,
                "system": 0.03,
                "child_user": 0,
                "user": 0.09,
                "child_sys": 0
            },
            "2020-06-22T15:09:30+09:00": {
                "iowait": 0,
                "percent": 36.47,
                "system": 0.13,
                "child_user": 0,
                "user": 10.81,
                "child_sys": 0
            },
            "2020-06-22T15:05:00+09:00": {
                "iowait": 0,
                "percent": 0.37,
                "system": 0.01,
                "child_user": 0,
                "user": 0.1,
                "child_sys": 0
            },
            "2020-06-22T15:06:00+09:00": {
                "iowait": 0,
                "percent": 0.6,
                "system": 0.04,
                "child_user": 0,
                "user": 0.14,
                "child_sys": 0
            },
            "2020-06-22T15:00:30+09:00": {
                "iowait": 0,
                "percent": 37.83,
                "system": 0.15,
                "child_user": 0,
                "user": 11.2,
                "child_sys": 0
            },
            "2020-06-22T15:04:00+09:00": {
                "iowait": 0,
                "percent": 0.4,
                "system": 0.03,
                "child_user": 0,
                "user": 0.09,
                "child_sys": 0
            },
            "2020-06-22T15:06:30+09:00": {
                "iowait": 0,
                "percent": 36.23,
                "system": 0.15,
                "child_user": 0,
                "user": 10.72,
                "child_sys": 0
            },
            "2020-06-22T15:03:00+09:00": {
                "iowait": 0,
                "percent": 0.4,
                "system": 0.02,
                "child_user": 0,
                "user": 0.1,
                "child_sys": 0
            },
            "2020-06-22T15:05:30+09:00": {
                "iowait": 0,
                "percent": 39.1,
                "system": 0.19,
                "child_user": 0,
                "user": 11.54,
                "child_sys": 0
            }
          },
          "tags": {
            "pid": "23251",
            "metric": "proc_cpu",
            "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
            "name": "influxd"
          }
        }
      }
 


   :queryparam string start: * **(필수)** 가져올 데이터 시작 시간 
      * ``YYYY-MM-DDThh:mm:ss+09:00`` iso8601형식
   :queryparam string end: * **(선택)** 가져올 데이터 끝 시간
      * ``YYYY-MM-DDThh:mm:ss+09:00`` iso8601형식
      * 미입력시 default는 ``0``. (현재시간)
   :queryparam string <metric>: * **(필수)** 가져올 메트릭 선택 가능
      * (proc_cpu/proc_mem/proc_diskio) 중 택1
   :queryparam int pid: * **(필수)** process-id
   :queryparam string aggr: * **(선택)** 메트릭 집계 데이타
      * (5m/1h/1d) 중 택1 ``5m``: 5분집계, ``1h``: 1시간집계, ``1d``: 1일집계
      * 미입력시 default는 ``None``.


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _get_metrics_alert:

.. http:get:: /api/metrics/hid/alert

   * <hid> 메트릭에 설정된 alert 정보 얻기

   **요청 예**:

   .. sourcecode:: http

      GET /api/metrics/BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE/alert HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "alerts": {
          "CPU": [
            {
              "detect_count": 3,
              "device": "cpu_t",
              "high": 30.0,
              "metric": "idle",
              "middle": 40.0,
              "reverse": "Y",
              "send_day_max": 3,
              "send_interval": 180,
              "sender_id": 1
            }
          ],
          "DISK": [
            {
              "detect_count": 3,
              "device": "vdb1",
              "high": 80.0,
              "metric": "percent",
              "middle": 70.0,
              "reverse": "N",
              "send_day_max": 3,
              "send_interval": 180,
              "sender_id": 1
            }
          ],
          "MEM": [
            {
              "detect_count": 3,
              "device": "ALL",
              "high": 85.0,
              "metric": "percent",
              "middle": 75.0,
              "reverse": "N",
              "send_day_max": 3,
              "send_interval": 180,
              "sender_id": 1
            }
          ],
          "NETWORK": [
            {
              "detect_count": 3,
              "device": "ens3",
              "high": 1000000.0,
              "metric": "inbps",
              "middle": 800000.0,
              "reverse": "N",
              "send_day_max": 3,
              "send_interval": 180,
              "sender_id": 1
            }
          ],
          "OFF": [
            {
              "detect_count": 3,
              "sender_id": 1
            }
          ],
          "SYSTEM": [
            {
              "detect_count": 3,
              "device": "ALL",
              "high": 30.0,
              "metric": "load1",
              "middle": 10.0,
              "reverse": "N",
              "send_day_max": 3,
              "send_interval": 180,
              "sender_id": 1
            }
          ]
        }
      }

   * **device**  해당서버에서 사용되는 디바이스
   * **metric**  해당 디바이스에 모니터링 상세항목
   * **reverse** 모니터링 대상 값이 클수록 위험이면 'N', 작을수록 위험이면 'Y' 으로 일반적으로 'N' 으로 설정됨.
   * **high**    모니터링 대상 값이 위험레벨 값
   * **middle**  모니터링 대상 값이 경고레벨 값
   * **detect_count**  모니터링 대상 조건에 감지 횟수 (횟수 만큼 감지되면 알람 발생됨 - 지속적인 위험을 체크하기 위함)
   * **send_interval** 알람전송후 다시 전송될 최소한의 간격을 지정함. (기본값 3분)
   * **send_day_max**  알람 전송 횟수를 하루 최대 횟수 설정. (SMS, Email, Slack 등등)
   * **sender_id**     해당 알람을 전송 대상 목록이 정의된 ID 값
   

   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _post_metrics_alert:

.. http:post:: /api/metrics/hid/alert

   * <hid> 메트릭에 새로운 alert 정보 추가 및 변경하기

   **요청 예**:

   .. sourcecode:: http

      POST /api/metrics/BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE/alert HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      {
        "CPU": [
          {
            "detect_count": 3,
            "device": "cpu_t",
            "high": 30.0,
            "metric": "idle",
            "middle": 40.0,
            "reverse": "Y",
            "send_day_max": 3,
            "send_interval": 180,
            "sender_id": 1
          }
        ],
        "DISK": [
          {
            "detect_count": 3,
            "device": "vdb1",
            "high": 80.0,
            "metric": "percent",
            "middle": 70.0,
            "reverse": "N",
            "send_day_max": 3,
            "send_interval": 180,
            "sender_id": 1
          }
        ]
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





.. _delete_metrics_alert:

.. http:delete:: /api/metrics/hid/alert

   * <hid> 메트릭에 기존 alert 정보 삭제하기

   **요청 예**:

   .. sourcecode:: http

      DELETE /api/metrics/BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE/alert HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 삭제정보

      {
        "CPU": [
          {
            "detect_count": 3,
            "device": "cpu_t",
            "high": 30.0,
            "metric": "idle",
            "middle": 40.0,
            "reverse": "Y",
            "send_day_max": 3,
            "send_interval": 180,
            "sender_id": 1
          }
        ]
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


