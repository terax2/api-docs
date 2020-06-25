======================
ixMonitor - Events API
======================


API List
========

+----------------------------------------------------------+-----------------------------------------------------+
|Endpoint                                                  |Description                                          |
+==========================================================+=====================================================+
|:ref:`GET /api/events/api-key/list <get_event_list>`      |<api-key>로 등록된 호스트들의 이벤트 정보 얻기       |
+----------------------------------------------------------+-----------------------------------------------------+


API Contents
============

.. _get_event_list:

.. http:post:: /api/events/api-key/list

   <api-key>로 등록된 호스트들의 이벤트 정보 얻기

   **요청 예**:

   .. sourcecode:: http

      GET /api/events/7E717E82ED7FB134/list?start=2020-06-25T00:00:00+09:00  HTTP/1.1
      Host: example.com
      Authorization: Basic eyJhbGciOiJIUzI1NiIsImV4cCI6MTU4NjIyNDMwMywiaWF0IjoxNTg2MjIzNzAzfQ.eyJ1c2VybmFtZSI6InRlcmF4In0.TxW3-HtKBOqJcDgS8gxGykdCP7GnZuVbRSD5UBzVyXw

   **응답 예**:

   .. sourcecode:: http

      HTTP/1.1 200 OK
      Content-Type: application/json

      {
        "data": {
          "events": [
            {
              "device": "ALL",
              "end": "2020-06-25T00:08:30+09:00",
              "event_id": 16358,
              "hostname": "kde-r1-dev",
              "level": "Warning",
              "limit": 10.0,
              "message": "hostname : [kde-r1-dev] system > load1, [3.50] ë¥¼ ì´ˆê³¼ í•˜ì˜€ìŠµë‹ˆë‹¤.",
              "metric": "load1",
              "pkey": "SYSTEM",
              "start": "2020-06-25T00:07:30+09:00",
              "status": "AutoCompleted",
              "value": 13.0
            },
            {
              "device": "ALL",
              "end": "2020-06-25T00:13:30+09:00",
              "event_id": 16360,
              "hostname": "kde-r1-dev",
              "level": "Warning",
              "limit": 10.0,
              "message": "hostname : [kde-r1-dev] system > load1, [0.50] ë¥¼ ì´ˆê³¼ í•˜ì˜€ìŠµë‹ˆë‹¤.",
              "metric": "load1",
              "pkey": "SYSTEM",
              "start": "2020-06-25T00:12:30+09:00",
              "status": "AutoCompleted",
              "value": 10.0
            },
            {
              "device": "ALL",
              "end": "2020-06-25T00:29:30+09:00",
              "event_id": 16362,
              "hostname": "kde-r1-dev",
              "level": "Warning",
              "limit": 10.0,
              "message": "hostname : [kde-r1-dev] system > load1, [7.50] ë¥¼ ì´ˆê³¼ í•˜ì˜€ìŠµë‹ˆë‹¤.",
              "metric": "load1",
              "pkey": "SYSTEM",
              "start": "2020-06-25T00:27:30+09:00",
              "status": "AutoCompleted",
              "value": 17.0
            },
            {
              "device": "ALL",
              "end": "2020-06-25T01:56:30+09:00",
              "event_id": 16364,
              "hostname": "kde-r1-dev",
              "level": "Warning",
              "limit": 10.0,
              "message": "hostname : [kde-r1-dev] system > load1, [1.75] ë¥¼ ì´ˆê³¼ í•˜ì˜€ìŠµë‹ˆë‹¤.",
              "metric": "load1",
              "pkey": "SYSTEM",
              "start": "2020-06-25T01:55:30+09:00",
              "status": "AutoCompleted",
              "value": 12.0
            },
            {
              "device": "ALL",
              "end": "2020-06-25T03:30:30+09:00",
              "event_id": 16366,
              "hostname": "kde-r1-dev",
              "level": "Warning",
              "limit": 10.0,
              "message": "hostname : [kde-r1-dev] system > load1, [3.25] ë¥¼ ì´ˆê³¼ í•˜ì˜€ìŠµë‹ˆë‹¤.",
              "metric": "load1",
              "pkey": "SYSTEM",
              "start": "2020-06-25T03:29:30+09:00",
              "status": "AutoCompleted",
              "value": 13.0
            },
            {
              "device": "ALL",
              "end": "2020-06-25T03:32:30+09:00",
              "event_id": 16368,
              "hostname": "kde-r1-dev",
              "level": "Warning",
              "limit": 10.0,
              "message": "hostname : [kde-r1-dev] system > load1, [0.25] ë¥¼ ì´ˆê³¼ í•˜ì˜€ìŠµë‹ˆë‹¤.",
              "metric": "load1",
              "pkey": "SYSTEM",
              "start": "2020-06-25T03:31:30+09:00",
              "status": "AutoCompleted",
              "value": 10.0
            },
            {
              "device": "ALL",
              "end": "2020-06-25T03:58:30+09:00",
              "event_id": 16370,
              "hostname": "kde-r1-dev",
              "level": "Warning",
              "limit": 10.0,
              "message": "hostname : [kde-r1-dev] system > load1, [0.75] ë¥¼ ì´ˆê³¼ í•˜ì˜€ìŠµë‹ˆë‹¤.",
              "metric": "load1",
              "pkey": "SYSTEM",
              "start": "2020-06-25T03:57:30+09:00",
              "status": "AutoCompleted",
              "value": 11.0
            },
            {
              "device": "ALL",
              "end": "2020-06-25T04:23:30+09:00",
              "event_id": 16372,
              "hostname": "kde-r1-dev",
              "level": "Alert",
              "limit": 30.0,
              "message": "hostname : [kde-r1-dev] system > load1, [4.50] ë¥¼ ì´ˆê³¼ í•˜ì˜€ìŠµë‹ˆë‹¤.",
              "metric": "load1",
              "pkey": "SYSTEM",
              "start": "2020-06-25T04:22:30+09:00",
              "status": "AutoCompleted",
              "value": 34.0
            },
            {
              "device": "ALL",
              "end": "2020-06-25T04:25:30+09:00",
              "event_id": 16374,
              "hostname": "kde-r1-dev",
              "level": "Warning",
              "limit": 10.0,
              "message": "hostname : [kde-r1-dev] system > load1, [0.50] ë¥¼ ì´ˆê³¼ í•˜ì˜€ìŠµë‹ˆë‹¤.",
              "metric": "load1",
              "pkey": "SYSTEM",
              "start": "2020-06-25T04:24:00+09:00",
              "status": "AutoCompleted",
              "value": 10.0
            },
            {
              "device": "ALL",
              "end": "2020-06-25T08:26:30",
              "event_id": 16376,
              "hostname": "kde-r1-dev",
              "level": "Warning",
              "limit": 10.0,
              "message": "hostname : [kde-r1-dev] system > load1, [6.75] ë¥¼ ì´ˆê³¼ í•˜ì˜€ìŠµë‹ˆë‹¤.",
              "metric": "load1",
              "pkey": "SYSTEM",
              "start": "2020-06-25T08:24:00",
              "status": "AutoCompleted",
              "value": 17.0
            }
          ],
          "page": "1/1",
          "tags": {
            "akey": "7E717E82ED7FB134"
          },
          "total": 10
        }
      }
 
   * **pkey**     알람 발생영역 구분 (SYSTEM, CPU, MEM, DISK, DISKIO, NETWORK, SYSLOG, APPLOG, PORT, CUSTOM)
   * **device**   해당 발생영역의 디바이스 정보 ('ALL' 해당 발생영역에는 디바이스 구분이 없다는 뜻)
   * **metric**   알람 발생영역의 상세 메트릭
   * **hostname** 알람 발생 서버의 호스트 네임
   * **level**    알람 발생 레벨 (Error, Warning)
   * **start**    알람 발생 시작 시간
   * **end**      알람 발생 종료 시간
   * **message**  알람 발생시 전송된 메세지
   * **value**    알람 발생시 메트리 값
   * **limit**    해당 메트릭의 임계치 값
   * **status**   알람 발생후 현재 상태 ('OnGoing : 진행중','AutoCompleted : 자연종료','ForceCompleted : 강제종료','TimeoutCompleted : 에이전트 OFF 이벤트 종료')
   * **event_id** 알람 발생 이벤트 번호 (알람 전송내역을 확인이 필요할 경우 사용됨)



   :queryparam string start: * **(필수)** 가져올 데이터 시작 시간 
      * ``YYYY-MM-DDThh:mm:ss+09:00`` iso8601형식
   :queryparam string end: * **(선택)** 가져올 데이터 끝 시간
      * ``YYYY-MM-DDThh:mm:ss+09:00`` iso8601형식
      * 미입력시 default는 ``0``. (현재시간)
   :queryparam string hid: * **(선택)** host-id
      * 미입력시 default는 ``None``. (api-key에 등록된 서버 전체 출력)
   :queryparam string pkey: * **(선택)** 이벤트 구분 코드
      * (CPU/MEM/DISK/DISKIO/NETWORK/SYSTEM/SYSLOG/APPLOG/PORT/CUSTOM/OFF/CUSTOM_OFF) 중 택1
      * 미입력시 default는 ``None``. (이벤트 전체대상)
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




