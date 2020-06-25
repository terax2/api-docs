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
        "hosts": [
          {
            "agent": "Online",
            "akey": "7E717E82ED7FB134",
            "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
            "hostname": "kde-r1-dev",
            "service": "Y",
            "status": "3",
            "system": "Linux"
          },
          {
            "agent": "Online",
            "akey": "7E717E82ED7FB134",
            "hid": "CB7A2A6E-102A-414C-8DBB-80AFCDC8C4FD",
            "hostname": "kde-r1-dev2",
            "service": "Y",
            "status": "3",
            "system": "Linux"
          },
          {
            "agent": "Online",
            "akey": "7E717E82ED7FB134",
            "hid": "CCA11FCF-87FC-4F0B-A1C0-E37C586CE6B7",
            "hostname": "test-dev",
            "service": "Y",
            "status": "3",
            "system": "Linux"
          }
        ]
      }
 

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
         "active_svc": "Y",
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
         "status": "3",
         "syslog_svc": "Y"
      }

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
   
   호스트의 서비스 및 수집주기 등 업데이트.

   **요청 예**:

   .. sourcecode:: http

      POST /api/basic/hostdetail?userid=xxx&hid=xxxxxxxxxxxxxxxxxxx HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: {
              "applog_svc": "Y",
              "syslog_svc": "Y",
              "custom_svc": "Y",
              "port_svc": "Y",
              "process_svc": "Y",
              "metric_int": 30,
              "hostname_alt": "host-update"
            }


   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "message": "Update OK"
      }

   :queryparam string userid: * **(필수)** user-id
   :queryparam string hid: * **(필수)** host-id
   :body:
      :string applog_svc: * **(선택)** application log 수집서비스 (Y/N)
         * 미입력시 default는 ``N``.
      :string syslog_svc: * **(선택)** syslog 수집서비스 (Y/N)
         * 미입력시 default는 ``N``.
      :string custom_svc: * **(선택)** custom script 실행서비스  (Y/N)
         * 미입력시 default는 ``N``.
      :string port_svc: * **(선택)** 특정포트 모니터링 실행서비스  (Y/N)
         * 미입력시 default는 ``N``.
      :string process_svc: * **(선택)** 프로세스별 모니터링 실행서비스  (Y/N)
         * 미입력시 default는 ``N``.
      :string metric_int: * **(선택)** 모든 메트릭의 수집 주기 설정
         * 미입력시 default는 ``60``.
      :string hostname_alt: * **(선택)** 해당서버의 호스트네임의 다른이름 설정
         * 미입력시 default는 ``None``.


   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류

