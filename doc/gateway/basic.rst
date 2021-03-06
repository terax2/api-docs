=====================
ixMonitor - Basic API
=====================


API List
========

+----------------------------------------------------------------------+-----------------------------------------------+
|Endpoint                                                              |Description                                    |
+======================================================================+===============================================+
|:ref:`GET /api/basic/account <get_basic_account>`                     |기본 계정 확인하기                             |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`POST /api/basic/account <post_basic_account>`                   |기본 계정 생성하기                             |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`POST /api/basic/apikey <post_basic_apikey>`                     |메트릭 및 로그 에이전트용 Api-key 생성하기     |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`GET /api/basic/hostlist <get_basic_hostlist>`                   |계정에 등록된 호스트 서버 목록 확인            |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`GET /api/basic/hostgroups <get_basic_hostgroups>`               |계정에 등록된 호스트 그룹 목록                 |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`POST /api/basic/hostgroups <post_basic_hostgroups>`             |계정에 등록된 호스트 그룹 수정                 |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`DELETE /api/basic/hostgroups <delete_basic_hostgroups>`         |계정에 등록된 호스트 그룹 삭제                 |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`POST /api/basic/hostgrpchg <post_basic_hostgrpchg>`             |계정에 등록된 호스트 그룹 변경                 |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`GET /api/basic/hostdetail <get_basic_hostdetail>`               |호스트 상세 내역 확인하기                      |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`POST /api/basic/hostdetail <post_basic_hostdetail>`             |호스트의 서비스 및 수집주기 등 업데이트        |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`GET /api/basic/templetelist <get_basic_templetelist>`           |계정내 템플릿 리스트                           |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`POST /api/basic/templetelist <post_basic_templetelist>`         |계정내 템플릿 수정,추가                        |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`DELETE /api/basic/templetelist <delete_basic_templetelist>`     |계정내 템플릿 삭제                             |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`GET /api/basic/templetegroups <get_basic_templetegroups>`       |계정내 템플릿 그룹 리스트                      |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`POST /api/basic/templetegroups <post_basic_templetegroups>`     |계정내 템플릿 그룹 수정,추가                   |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`DELETE /api/basic/templetegroups <delete_basic_templetegroups>` |계정내 템플릿 그룹 삭제                        |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`GET /api/basic/serviceupdate <get_basic_serviceupdate>`         |계정내 서비스 내용 보기                        |
+----------------------------------------------------------------------+-----------------------------------------------+
|:ref:`POST /api/basic/serviceupdate <post_basic_serviceupdate>`       |계정내 서비스 내용 수정                        |
+----------------------------------------------------------------------+-----------------------------------------------+


API Contents
============

.. _get_basic_account:

.. http:get:: /api/basic/account

   기본 계정 확인하기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/basic/account?userid=xxx&passwd=xxxxx HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }

   :queryparam string userid: * **(필수)** user-id
   :queryparam string passwd: * **(필수)** password

   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류




.. _post_basic_account:

.. http:post:: /api/basic/account

   기본 계정 생성하기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/basic/account?userid=xxx&passwd=xxxxx HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }

   :queryparam string userid: * **(필수)** user-id
   :queryparam string passwd: * **(필수)** password

   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류




.. _post_basic_apikey:

.. http:post:: /api/basic/apikey
   
   메트릭 및 로그 에이전트용 Api-key 생성하기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/basic/apikey?userid=xxx HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "api-key":"7E717E82ED7FB134"
      }


   :queryparam string userid: * **(필수)** user-id
 
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류






.. _get_basic_hostlist:

.. http:get:: /api/basic/hostlist
   
   계정에 등록된 호스트 서버 목록 확인.

   **요청 예**:

   .. sourcecode:: http

      GET /api/basic/apikey?userid=xxx HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw



   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "7E717E82ED7FB134": [
          {
            "group_id": 1,
            "group_name": "기본그룹_수정",
            "hosts": [
              {
                "agent_status": "Online",
                "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
                "hostname": "kde-r1-dev",
                "server_status": "Normal",
                "service": "Online",
                "system": "Linux"
              },
              {
                "agent_status": "Online",
                "hid": "CCA11FCF-87FC-4F0B-A1C0-E37C586CE6B7",
                "hostname": "test-dev",
                "server_status": "Normal",
                "service": "Online",
                "system": "Linux"
              },
              {
                "agent_status": "Online",
                "hid": "CB7A2A6E-102A-414C-8DBB-80AFCDC8C4FD",
                "hostname": "kde-r1-dev2",
                "server_status": "Normal",
                "service": "Online",
                "system": "Linux"
              }
            ]
          },
          {
            "group_id": 2,
            "group_name": "그룹2",
            "hosts": []
          }
        ]
      }


   * **service**      해당 서비스 사용 유무 (에이전트가 설치되서 시작되면 활성화됨.)
   * **agent_status** 해당 서버의 에이전트 접속상태를 표시.
   * **akey**         에이전트를 시작하기 위한 api-key 값.(계정당 1개는 필수)
   * **hid**          해당서버의 Unique-ID 값 (에이전트 활성화시 자동으로 생성됨)
   * **hostname**     해당 서버의 호스트 네임(hostname_alt 값이 있을 경우에는 hostname_alt로 표시됨)
   * **system**       해당 서버의 OS 구분 ( Linux, Windows )
   * **status**       현재 해당 서버의 상태 (Normal, Warning, Alert)

   :queryparam string userid: * **(필수)** user-id
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류






.. _get_basic_hostgroups:

.. http:get:: /api/basic/hostgroups
   
   계정에 등록된 호스트 그룹 목록.

   **요청 예**:

   .. sourcecode:: http

      GET /api/basic/hostgroups?akey=7E717E82ED7FB134 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw



   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "groups": [
          {
            "group_id": 1,
            "group_name": "기본그룹"
          }
        ]
      }


   * **group_id**     기본그룹 ID (기본그룹은 무조건 존재함-삭제불가)
   * **group_name**   기본그룹 명

   :queryparam string akey: * **(필수)** api-key 값
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _post_basic_hostgroups:

.. http:post:: /api/basic/hostgroups
   
   계정에 등록된 호스트 그룹 수정.

   **요청 예**:

   .. sourcecode:: http

      POST /api/basic/hostgroups?akey=7E717E82ED7FB134 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      {
        "group_id": 1,
        "group_name": "그룹명"
      }

      * **group_id**      수정할 그룹ID (그룹ID 값이 없을 경우 그룹이 추가됨)


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }


   :queryparam string akey: * **(필수)** api-key 값
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _delete_basic_hostgroups:

.. http:delete:: /api/basic/hostgroups
   
   계정에 등록된 호스트 그룹 삭제.

   **요청 예**:

   .. sourcecode:: http

      DELETE /api/basic/hostgroups?akey=7E717E82ED7FB134 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      {
        "group_id": 1,
        "group_name": "그룹명"
      }


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }


   :queryparam string akey: * **(필수)** api-key 값
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _post_basic_hostgrpchg:

.. http:post:: /api/basic/hostgrpchg
   
   계정에 등록된 호스트 그룹 변경.

   **요청 예**:

   .. sourcecode:: http

      POST /api/basic/hostgroups?akey=7E717E82ED7FB134 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      [
        {
          "new_group_id": 1,
          "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE"
        }
      ]


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }


   :queryparam string akey: * **(필수)** api-key 값
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류







.. _get_basic_hostdetail:

.. http:get:: /api/basic/hostdetail
   
   호스트 상세 내역 확인하기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/basic/hostdetail?userid=xxx&hid=xxxxxxxxxxxxxxxxxxx HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "detail": {
          "agent_status": "Online",
          "service": "Y",
          "applog_svc": "Y",
          "assigned": "1.201.160.22:6929",
          "custom_svc": "Y",
          "hostname": "kde-r1-dev",
          "hostname_alt": null,
          "last_collect": "2020-06-23T10:04:30",
          "local_addrs": [
            {
              "lo": {
                "mac": "00:00:00:00:00:00",
                "tcp4": "127.0.0.1",
                "tcp6": "::1"
              }
            },
            {
              "ens3": {
                "mac": "fa:16:3e:2c:38:15",
                "tcp4": "192.168.10.17",
                "tcp6": "fe80::f816:3eff:fe2c:3815%ens3"
              }
            }
          ],
          "metric_int": 30,
          "os_detail": "Ubuntu 16.04 xenial",
          "os_system": "Linux",
          "port_svc": "Y",
          "process_svc": "Y",
          "remote_addr": "1.201.160.22",
          "status": "Normal",
          "syslog_svc": "Y"
        }
      }

   * **service**      해당 서비스 사용 유무 (에이전트가 설치되서 시작되면 활성화됨.)
   * **agent_status** 해당 서버의 에이전트 상태를 표시.
   * **applog_svc**   어플리케이션 로그 수집 기능 사용유무.(기본값 'N')
   * **syslog_svc**   시스템 로그 수집 기능 사용유무.(기본값 'N')
   * **custom_svc**   Custom Scripts 기능 사용유무.(기본값 'Y')
   * **port_svc**     Port 모니터링 기능 사용유무.(기본값 'Y')
   * **process_svc**  Process 모니터링 기능 사용유무.(기본값 'N')
   * **assigned**     에이전트가 활성화되면 최초에 한번 데이타 저장소가(위치) 설정됨.
   * **hostname**     해당 서버의 호스트 네임
   * **hostname_alt** 해당 서버의 호스트 네임 대신 사용할수 있는 별칭.(기본값 null)
   * **metric_int**   해당 서버에서 메트릭을 수집하는 주기 설정 (기본값 60초 설정, 30 ~ 60 초까지 초 단위 설정 가능)
   * **last_collect** 해당 서버에서 마지막으로 메트릭이 수집된 시간
   * **local_addrs**  해당 서버의 IP 정보
   * **os_system**    해당 서버의 OS 구분 ( Linux, Windows )
   * **os_detail**    해당 서버의 OS 상세정보
   * **remote_addr**  해당 서버가 접속된 원격지 공인 IP 
   * **status**       현재 해당 서버의 상태 (Normal, Warning, Alert)


   :queryparam string userid: * **(필수)** user-id
   :queryparam string hid: * **(필수)** host-id
 
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류



.. _post_basic_hostdetail:

.. http:post:: /api/basic/hostdetail
   
   * 호스트의 서비스 및 수집주기 등 업데이트.

   **요청 예**:

   .. sourcecode:: http

      POST /api/basic/hostdetail?userid=xxx&hid=xxxxxxxxxxxxxxxxxxx HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 업데이트 내용

      {
        "service"   : "Y",
        "applog_svc": "Y",
        "syslog_svc": "Y",
        "custom_svc": "Y",
        "port_svc": "Y",
        "process_svc": "Y",
        "metric_int": 30,
        "hostname_alt": "host-update"
      }

   * **service**      해당 서비스 사용 유무 (에이전트가 설치되서 시작되면 활성화됨.)
   * **applog_svc**   어플리케이션 로그 수집 기능 사용유무.(기본값 'N')
   * **syslog_svc**   시스템 로그 수집 기능 사용유무.(기본값 'N')
   * **custom_svc**   Custom Scripts 기능 사용유무.(기본값 'Y')
   * **port_svc**     Port 모니터링 기능 사용유무.(기본값 'Y')
   * **process_svc**  Process 모니터링 기능 사용유무.(기본값 'N')
   * **metric_int**   해당 서버에서 메트릭을 수집하는 주기 설정 (기본값 60초 설정, 30 ~ 60 초까지 초 단위 설정 가능)
   * **hostname_alt** 해당 서버의 호스트 네임 대신 사용할수 있는 별칭.(기본값 null)


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "Update OK"
      }

   :queryparam string userid: * **(필수)** user-id
   :queryparam string hid: * **(필수)** host-id


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류






.. _get_basic_templetelist:

.. http:get:: /api/basic/templetelist
   
   계정내 템플릿 리스트.

   **요청 예**:

   .. sourcecode:: http

      GET /api/basic/templetelist?akey=7E717E82ED7FB134 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw



   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "기본그룹": {
          "group_id": 1,
          "templetes": {
            "CPU": [
              {
                "detect_count": 3,
                "device": "cpu_t",
                "high": 40.0,
                "metric": "idle",
                "middle": 60.0,
                "reverse": "Y",
                "send_day_max": 3,
                "send_interval": 180
              }
            ],
            "DISK": [
              {
                "detect_count": 3,
                "device": "ALL",
                "high": 85.0,
                "metric": "percent",
                "middle": 70.0,
                "reverse": "N",
                "send_day_max": 3,
                "send_interval": 180
              }
            ],
            "DISKIO": [
              {
                "detect_count": 3,
                "device": "ALL",
                "high": 100000000.0,
                "metric": "write_bytes",
                "middle": 70000000.0,
                "reverse": "N",
                "send_day_max": 3,
                "send_interval": 180
              }
            ],
            "MEM": [
              {
                "detect_count": 3,
                "device": "ALL",
                "high": 80.0,
                "metric": "percent",
                "middle": 60.0,
                "reverse": "N",
                "send_day_max": 3,
                "send_interval": 180
              }
            ],
            "NETWORK": [
              {
                "detect_count": 3,
                "device": "ALL",
                "high": 500000000.0,
                "metric": "inbytes",
                "middle": 300000000.0,
                "reverse": "N",
                "send_day_max": 3,
                "send_interval": 180
              }
            ],
            "OFF": [
              {
                "detect_count": 3,
                "device": "ALL",
                "high": 0,
                "metric": "ALL",
                "middle": 0,
                "reverse": "N",
                "send_day_max": 3,
                "send_interval": 180
              }
            ],
            "SYSTEM": [
              {
                "detect_count": 3,
                "device": "ALL",
                "high": 60,
                "metric": "load1",
                "middle": 40,
                "reverse": "N",
                "send_day_max": 3,
                "send_interval": 180
              }
            ]
          }
        }
      }


   * **group_id**      기본그룹 ID
   * **templetes**     기본 템플릿 구성내용
     .. **category**      항목 구분 ('CPU', 'DISK', 'DISKIO', 'MEM', 'NETWORK', 'SYSTEM', 'OFF')
     .. **device**        디바이스
     .. **metric**        디바이스의 상세 항목
     .. **reverse**       'Y': 수치가 낮을수록 위험, 'N' : 수치가 높을수록 위험. (일반적으로 'N' 값이 기본값임)
     .. **high**          Alert - 경고 수치 값
     .. **middle**        Warning - 경고 수치 값
     .. **detect_count**  연속 감지 횟수
     .. **send_interval** 알람 발송 간격
     .. **send_day_max**  하루 최대 발송 횟수


   :queryparam string akey: * **(필수)** api-key 값
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _post_basic_templetelist:

.. http:post:: /api/basic/templetelist
   
   계정내 템플릿 수정,추가

   **요청 예**:

   .. sourcecode:: http

      POST /api/basic/templetelist?akey=7E717E82ED7FB134 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      {
        "group_id": 1,
        "templetes": {
          "CPU": [
            {
              "detect_count": 3,
              "device": "cpu_t",
              "high": 40.0,
              "metric": "idle",
              "middle": 60.0,
              "reverse": "Y",
              "send_day_max": 3,
              "send_interval": 180
            }
          ]
        }
      }

      * **group_id**      기본그룹 ID
      * **templetes**     기본 템플릿 구성내용
        .. **category**      항목 구분 ('CPU', 'DISK', 'DISKIO', 'MEM', 'NETWORK', 'SYSTEM', 'OFF')
        .. **device**        디바이스
        .. **metric**        디바이스의 상세 항목
        .. **reverse**       'Y': 수치가 낮을수록 위험, 'N' : 수치가 높을수록 위험. (일반적으로 'N' 값이 기본값임)
        .. **high**          Alert - 경고 수치 값
        .. **middle**        Warning - 경고 수치 값
        .. **detect_count**  연속 감지 횟수
        .. **send_interval** 알람 발송 간격
        .. **send_day_max**  하루 최대 발송 횟수


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }


   :queryparam string akey: * **(필수)** api-key 값
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _delete_basic_templetelist:

.. http:delete:: /api/basic/templetelist
   
   계정내 템플릿 삭제

   **요청 예**:

   .. sourcecode:: http

      DELETE /api/basic/templetelist?akey=7E717E82ED7FB134 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      {
        "group_id": 1,
      }

      * **group_id**      기본그룹 ID


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }


   :queryparam string akey: * **(필수)** api-key 값
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류







.. _get_basic_templetegroups:

.. http:get:: /api/basic/templetegroups
   
   계정내 템플릿 그룹 리스트.

   **요청 예**:

   .. sourcecode:: http

      GET /api/basic/templetegroups?akey=7E717E82ED7FB134 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "groups": [
          {
            "group_id": 1,
            "group_name": "기본그룹"
          }
        ]
      }

   :queryparam string akey: * **(필수)** api-key 값
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _post_basic_templetegroups:

.. http:post:: /api/basic/templetegroups
   
   계정내 템플릿 그룹 수정,추가

   **요청 예**:

   .. sourcecode:: http

      POST /api/basic/templetegroups?akey=7E717E82ED7FB134 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      {
        "group_id": 1,
        "group_name": "그룹추가"
      }

      * **group_id**      수정할 그룹ID (그룹ID 값이 없을 경우 그룹이 추가됨)

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }


   :queryparam string akey: * **(필수)** api-key 값
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _delete_basic_templetegroups:

.. http:delete:: /api/basic/templetegroups
   
   계정내 템플릿 삭제

   **요청 예**:

   .. sourcecode:: http

      DELETE /api/basic/templetelist?akey=7E717E82ED7FB134 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      {
        "group_id": 1,
      }

      * **group_id**      기본그룹 ID


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }


   :queryparam string akey: * **(필수)** api-key 값
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류






.. _get_basic_serviceupdate:

.. http:get:: /api/basic/serviceupdate
   
   계정내 서비스 내용 보기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/basic/serviceupdate?akey=7E717E82ED7FB134 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "services": [
          {
            "applog": "Y",
            "custom": "Y",
            "group_name": "기본그룹",
            "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
            "hostname": "kde-r1-dev",
            "interval": 30,
            "monitoring": "Y",
            "port": "Y",
            "process": "Y",
            "syslog": "Y"
          },
          {
            "applog": "Y",
            "custom": "Y",
            "group_name": "기본그룹",
            "hid": "CCA11FCF-87FC-4F0B-A1C0-E37C586CE6B7",
            "hostname": "test-dev",
            "interval": 60,
            "monitoring": "Y",
            "port": "Y",
            "process": "Y",
            "syslog": "Y"
          },
          {
            "applog": "Y",
            "custom": "Y",
            "group_name": "기본그룹",
            "hid": "CB7A2A6E-102A-414C-8DBB-80AFCDC8C4FD",
            "hostname": "kde-r1-dev2",
            "interval": 60,
            "monitoring": "Y",
            "port": "Y",
            "process": "Y",
            "syslog": "Y"
          }
        ]
      }

   :queryparam string akey: * **(필수)** api-key 값
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _post_basic_serviceupdate:

.. http:post:: /api/basic/serviceupdate
   
   계정내 서비스 내용 수정

   **요청 예**:

   .. sourcecode:: http

      POST /api/basic/serviceupdate?akey=7E717E82ED7FB134 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 수정 정보

      [
        {
          "applog": "Y",
          "custom": "Y",
          "hid": "CCA11FCF-87FC-4F0B-A1C0-E37C586CE6B7",
          "interval": 60,
          "monitoring": "Y",
          "port": "Y",
          "process": "Y",
          "syslog": "Y"
        }
      ]

      * **hid**      호스트 ID 값은 반드시 필요 합니다.

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "OK"
      }


   :queryparam string akey: * **(필수)** api-key 값
  
   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류
