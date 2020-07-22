=======================
ixMonitor - Customs API
=======================


API List
========

+-----------------------------------------------------------------+-------------------------------------------------------+
|Endpoint                                                         |Description                                            |
+=================================================================+=======================================================+
|:ref:`GET /api/customs/hid/scripts <get_customs_scripts>`        |<hid>에 설정된 Customs Scripts 정보 얻기               |
+-----------------------------------------------------------------+-------------------------------------------------------+
|:ref:`POST /api/customs/hid/scripts <post_customs_scripts>`      |<hid>에 설정된 Customs Scripts 추가,변경 하기          |
+-----------------------------------------------------------------+-------------------------------------------------------+
|:ref:`DELETE /api/customs/hid/scripts <delete_customs_scripts>`  |<hid>에 설정된 Customs Scripts 정보 삭제 하기          |
+-----------------------------------------------------------------+-------------------------------------------------------+
|:ref:`GET /api/customs/api-key/alert <get_customs_alerts>`       |<api-key>에 설정된 Customs alert 정보 얻기             |
+-----------------------------------------------------------------+-------------------------------------------------------+
|:ref:`POST /api/custom/api-key/alert <post_customs_alerts>`      |<api-key>에 설정된 Customs alert 정보 추가 및 변경하기 |
+-----------------------------------------------------------------+-------------------------------------------------------+
|:ref:`DELETE /api/customs/api-key/alert <delete_customs_alerts>` |<api-key>에 설정된 Customs alert 정보 삭제하기         |
+-----------------------------------------------------------------+-------------------------------------------------------+



API Contents
============

.. _get_customs_scripts:

.. http:get:: /api/customs/hid/scripts

   * <hid>에 등록된 Customs Scripts 정보 얻기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/customs/BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE/scripts  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "customs": {
          "cmd.ls": {
            "active": "Y",
            "args": [],
            "custom_id": 1,
            "return_type": "string",
            "scripts": "ls -al |wc -l",
            "scripts_type": "cmd"
          },
          "cmd.test": {
            "active": "Y",
            "args": [],
            "custom_id": 4,
            "return_type": "value",
            "scripts": "/ixMonitor/Common-Gateway/test.py",
            "scripts_type": "cmd"
          },
          "host.ls": {
            "active": "Y",
            "args": [
              "1",
              "2"
            ],
            "custom_id": 2,
            "return_type": "value",
            "scripts": "#!/bin/bash\r\n\r\nvalue=`ls -al |wc -l`\r\necho $value",
            "scripts_type": "shell"
          },
          "python.test": {
            "active": "Y",
            "args": [],
            "custom_id": 3,
            "return_type": "value",
            "scripts": "#!/usr/bin/env python\r\n#-*- coding: utf-8 -*-\r\n\r\nimport os, sys\r\nimport subprocess\r\n\r\n\r\ndef main():\r\n\r\n    result  = subprocess.check_output('ls -al | wc -l', shell=True)\r\n    r_value = result.replace('\\n','')\r\n    print r_value\r\n    return\r\n\r\n\r\nif __name__ == '__main__':\r\n    sys.exit(main())\r\n",
            "scripts_type": "python"
          }
        }
      }

   * **scripts_type** 스크립트 타입 [shell | python | cmd] 중 하나임.
   * **args**         스크립트가 실행될때 전달되는 파라미터 값
   * **scripts**      실제 수행되는 스크립트 코드 자체.
   * **return_type**  스크립트 실행된 결과가 string 인지 value 인지 구분
   * **custom_id**    화면상에서는 보이지 않음.  alert 내용을 수정하거나 삭제할때 반드시 필요 함.  만약에 POST 상태에서 custom_id 값이 없을 경우에는 신규추가 처리됨.



   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _post_customs_scripts:

.. http:post:: /api/customs/hid/scripts

   * <hid>에 등록된 Customs Scripts 정보 추가,변경 하기.

   **요청 예**:

   .. sourcecode:: http

      POST /api/customs/BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE/scripts  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      {
        "cmd.ls": {
          "active": "Y",
          "args": [],
          "custom_id": 1,
          "return_type": "string",
          "scripts": "ls -al |wc -l",
          "scripts_type": "cmd"
        },
        "new.scripts": {
          "active": "Y",
          "args": [],
          "return_type": "string",
          "scripts": "ls -al |wc -l",
          "scripts_type": "cmd"
        }
      }

   * **scripts_type** 스크립트 타입 [shell | python | cmd] 중 하나임.
   * **args**         스크립트가 실행될때 전달되는 파라미터 값
   * **scripts**      실제 수행되는 스크립트 코드 자체.
   * **return_type**  스크립트 실행된 결과가 string 인지 value 인지 구분
   * **custom_id**    화면상에서는 보이지 않음.  alert 내용을 수정하거나 삭제할때 반드시 필요 함.  만약에 POST 상태에서 custom_id 값이 없을 경우에는 신규추가 처리됨.


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





.. _delete_customs_scripts:

.. http:delete:: /api/customs/hid/scripts

   * <hid>에 등록된 Customs Scripts 정보 삭제 하기.

   **요청 예**:

   .. sourcecode:: http

      DELETE /api/customs/BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE/scripts  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 삭제 정보

      {
        "cmd.ls": {
          "custom_id": 1
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





.. _get_customs_alerts:

.. http:get:: /api/customs/hid/alerts

   * <api-key>에 설정된 Customs alert 정보 얻기.

   **요청 예**:

   .. sourcecode:: http

      GET /api/customs/7E717E82ED7FB134/alerts?group_id=1 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "alerts": [
          {
            "custom_id": 1,
            "detect_count": 3,
            "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
            "high": 0,
            "hostname": "kde-r1-dev",
            "middle": 0,
            "result": "24",
            "return_type": "string",
            "send_day_max": 3,
            "send_interval": 180,
            "sender_id": 1
          },
          {
            "custom_id": 2,
            "detect_count": 3,
            "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
            "high": 45.0,
            "hostname": "kde-r1-dev",
            "middle": 35.0,
            "result": "",
            "return_type": "value",
            "send_day_max": 3,
            "send_interval": 180,
            "sender_id": 1
          },
          {
            "custom_id": 3,
            "detect_count": 3,
            "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
            "high": 60.0,
            "hostname": "kde-r1-dev",
            "middle": 30.0,
            "result": "",
            "return_type": "value",
            "send_day_max": 3,
            "send_interval": 180,
            "sender_id": 1
          },
          {
            "custom_id": 4,
            "detect_count": 3,
            "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
            "high": 50.0,
            "hostname": "kde-r1-dev",
            "middle": 30.0,
            "result": "",
            "return_type": "value",
            "send_day_max": 3,
            "send_interval": 180,
            "sender_id": 1
          },
          {
            "custom_id": 618768,
            "detect_count": 3,
            "hid": "BA498C9B-5C8C-4881-A4A6-6FE9074BB8DE",
            "high": 0,
            "hostname": "kde-r1-dev",
            "middle": 0,
            "result": "24",
            "return_type": "string",
            "send_day_max": 3,
            "send_interval": 180,
            "sender_id": 1
          }
        ]
      }

   * **custom_id**     고객이 정의한 Custom Scipts 등록 번호(alert 내용을 수정하거나 삭제할때 반드시 필요 함)
   * **return_type**   스크립트 실행결과 값 타입 구분 (string | value)
   * **result**        return_type 이 string 일 경우: 모니터링 대상 값에 해당하는 매칭 문자 (regular expression 가능)
   * **high**          return_type 이 value 일 경우 : 모니터링 대상 값이 위험레벨 값
   * **middle**        return_type 이 value 일 경우 : 모니터링 대상 값이 경고레벨 값
   * **detect_count**  모니터링 대상 조건에 감지 횟수 (횟수 만큼 감지되면 알람 발생됨 - 지속적인 위험을 체크하기 위함)
   * **send_interval** 알람전송후 다시 전송될 최소한의 간격을 지정함. (기본값 3분)
   * **send_day_max**  알람 전송 횟수를 하루 최대 횟수 설정. (SMS, Email, Slack 등등)
   * **sender_id**     해당 알람을 전송 대상 목록이 정의된 ID 값
   
   :queryparam int group_id: * **(필수)** 호스트 그룹ID
   :queryparam string hid: * **(선택)** host-id
      * 미입력시 default는 ``None``. (api-key에 등록된 서버 전체 출력)

   :resheader Content-Type: json만을 지원
   :statuscode 200: no error
   :statuscode 204: 해당 데이터가 없음
   :statuscode 400: 요청 파라미터 오류
   :statuscode 401: Token이 expire되거나, 올바르지 않음
   :statuscode 405: 내부 서버 오류





.. _post_customs_alerts:

.. http:post:: /api/customs/api-key/alerts

   * <api-key>에 설정된 Customs alert 정보 추가 및 변경하기

   **요청 예**:

   .. sourcecode:: http

      POST /api/customs/7E717E82ED7FB134/alerts?group_id=1 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 추가,수정 정보

      [
        {
          "custom_id": 2,
          "detect_count": 3,
          "high": 45.0,
          "middle": 35.0,
          "return_type": "value",
          "send_day_max": 3,
          "send_interval": 180,
          "sender_id": 1
        },
        {
          "custom_id": 4,
          "detect_count": 3,
          "high": 50.0,
          "middle": 30.0,
          "return_type": "value",
          "send_day_max": 3,
          "send_interval": 180,
          "sender_id": 1
        }
      ]


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





.. _delete_customs_alerts:

.. http:delete:: /api/customs/api-key/alerts

   * <api-key>에 설정된 Customs alert 정보 삭제하기.

   **요청 예**:

   .. sourcecode:: http

      DELETE /api/customs/7E717E82ED7FB134/alerts?group_id=1 HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw
      body: 삭제정보

      [
        {
          "custom_id": 2,
          "detect_count": 3,
          "high": 45.0,
          "middle": 35.0,
          "return_type": "value",
          "send_day_max": 3,
          "send_interval": 180,
          "sender_id": 1
        }
      ]


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
