=====================
ixMonitor - Basic API
=====================


API List
========

+----------------------------------------------------------+-----------------------------------------------+
|Endpoint                                                  |Description                                    |
+==========================================================+===============================================+
|:ref:`GET /api/basic/account <get_basic_account>`         |기본 계정 확인하기                             |
+----------------------------------------------------------+-----------------------------------------------+
|:ref:`POST /api/basic/account <post_basic_account>`       |기본 계정 생성하기                             |
+----------------------------------------------------------+-----------------------------------------------+
|:ref:`POST /api/basic/apikey <post_basic_apikey>`         |메트릭 및 로그 에이전트용 Api-key 생성하기     |
+----------------------------------------------------------+-----------------------------------------------+
|:ref:`GET /api/basic/hostlist <get_basic_hostlist>`       |계정에 등록된 호스트 서버 목록 확인            |
+----------------------------------------------------------+-----------------------------------------------+
|:ref:`GET /api/basic/hostdetail <get_basic_hostdetail>`   |호스트 상세 내역 확인하기                      |
+----------------------------------------------------------+-----------------------------------------------+
|:ref:`POST /api/basic/hostdetail <post_basic_hostdetail>` |호스트의 서비스 및 수집주기 등 업데이트        |
+----------------------------------------------------------+-----------------------------------------------+


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
        "UUID":"7E717E82ED7FB134"
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
        "akey": "7E717E82ED7FB134",
        "hosts": [
          {
            "agent_status": "Online",
            "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
            "hostname": "kde-r1-dev",
            "service": "Y",
            "status": "Normal",
            "system": "Linux"
          },
          {
            "agent_status": "Online",
            "hid": "CB7A2A6E-102A-414C-8DBB-80AFCDC8C4FD",
            "hostname": "kde-r1-dev2",
            "service": "Y",
            "status": "Normal",
            "system": "Linux"
          },
          {
            "agent_status": "Online",
            "hid": "CCA11FCF-87FC-4F0B-A1C0-E37C586CE6B7",
            "hostname": "test-dev",
            "service": "Y",
            "status": "Normal",
            "system": "Linux"
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
   * **status**       현재 해당 서버의 상태


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

