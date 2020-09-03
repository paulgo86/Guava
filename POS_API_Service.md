작업 내용 정리

# GUAVA POS에 서비스중인 API
---

# 모듈 : http_api

---

## 1. 전체 업체 카운트

> 데이터베이스에 등록된 업체의 `수`를 조회한다.

---

- PATH
> '/'

- METHOD
> GET

- PARAMETER
> [ none ]

- RETURN
```
{
    cnt: 등록 업체 수,
    req: 요청객체.body,
    msg: 'http api server for win XP client'
}
```

---

## 2. 특정 업체 상세 정보 조회

> 요청 파라미터의 사업자 번호로 등록된 업체의 `상세 정보`를 조회한다.

---

- PATH
> '/'

- METHOD
> POST

- PARAMETER
```
{
    bsNum: 사업자 번호
}
```

- RETURN
```
{
    result:1,
    data:해당 사업자 번호로 등록된 업체의 정보,
    msg:'http api server for win XP client'
}
```


---

## 3. 주차장 유무 정보 설정

> 업체의 `주차장 유무 정보`를 설정한다.

---

- PATH
> '/setParking'

- METHOD
> POST

- PARAMETER
```
{
    bsNum:사업자 번호,
    park: 주차장 유무 ( 1:유, 0:무 )
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러, 3:입력값 없음, 4: 업체 없음 )
    msg: 처리 결과 메세지,
    data: 수정된 업체 데이터
}
```

---

## 4. 업체 전화번호 설정

> 업체의 `전화번호`를 설정한다.

---

- PATH
> '/setBsTel'

- METHOD
> POST

- PARAMETER
```
{
    bsNum: 사업자 번호,
    bsTel: 설정할 전화번호
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러, 3:입력값 없음, 4: 업체 없음 )
    msg: 처리 결과 메세지,
    data: 수정된 업체 데이터
}
```


---

## 5. 업체 영업일 설정

> 업체의 영업일을 설정한다.
>
> ( `'yyyynny'` 와 같은 `요일 코드`를 받아서 처리 )

---

- PATH
> '/setBsDay'

- METHOD
> POST

- PARAMETER
```
{
    bsNum: 사업자 번호,
    bsDay: 요일, ( 요일로 온 경우 코드로 변환함 )
    [ 요일코드만 사용하게 변경됨 ]
    bsDayCode: 요일코드,
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러, 3:입력값 없음, 4: 업체 없음 )
    msg: 처리 결과 메세지,
    data: 수정된 업체 데이터, 요청한 요일코드
}
```


---

## 6. 업체 영업시간 설정

> 업체의 `영업 시간` ( 오픈 / 클로즈 ) 을 설정한다.

---

- PATH
> '/setBsHour'

- METHOD
> POST

- PARAMETER
```
{
    bsNum: 사업자 번호,
    open: 영업시작시간,
    close: 영업마감시간,
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러, 3:입력값 없음, 4: 업체 없음 )
    msg: 처리 결과 메세지,
    data: 수정된 업체 데이터, 요청한 요일코드
}
```

---

## 7. 업체 정보 조회

> 요청 파라미터의 사업자 번호로 등록된 `업체의 정보`를 조회한다.

---

- PATH
> '/view'

- METHOD
> POST

- PARAMETER
```
{
    bsNum: 사업자 번호,
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러, 3:입력값 없음, 4: 업체 없음 )
    msg: 처리 결과 메세지,
    data: 수정된 업체 데이터, 요청한 요일코드
}
```



---

## 8. 업체 영업상태 설정

> 해당 업체의 `영업상태`를 변경하고 상태변경 푸시알림을 전송한다.
>
> 변경작업에 대한 결과를 리턴한다.

---

- PATH
> '/status'

- METHOD
> POST

- PARAMETER
```
{
    bsNum: 사업자 번호,
    statusCode
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러, 3:입력값 없음, 4: 업체 없음 )
    msg: 처리 결과 메세지,
    data: 수정된 업체 데이터
}
```

---

## 9. 업체 공휴일 설정

> 해당 업체의 `공휴일`을 설정한다.

---

- PATH
> '/holiday'

- METHOD
> POST

- PARAMETER
```
{
    bsNum: 사업자 번호,
    holidayFrom: 휴가 시작일,
    holidayTo: 휴가 종료일,
    ( 일자 형태 `yyyy-mm-dd` )
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러, 3:입력값 없음, 4: 업체 없음 )
    msg: 처리 결과 메세지,
    data: 수정된 업체 데이터
}
```

---

## 10. 업체 영업상태 설정- 조기마감

> 해당 업체의 영업상태를 `조기 마감` 상태로 변경하고,
> 
> 기존 영업마감시간이 되면 영업종료 상태로 변경하는 타이머 등록

---

- PATH
> '/earlyClosing'

- METHOD
> POST

- PARAMETER
```
{
    bsNum: 사업자 번호,
    reason: 조기마감 사유,
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러, 3:입력값 없음, 4: 업체 없음 )
    msg: 처리 결과 메세지,
    data: 수정된 업체 데이터
}
```


---

## 11. 업체 브레이크
> 해당 업체의 영업상태를 `브레이크` 상태로 변경하고
>
> 브레이크 시간후에 다시 영업상태로 변경하는 타이머 등록

---

- PATH
> '/break'

- METHOD
> POST

- PARAMETER
```
{
    bsNum: 사업자 번호,
    breakExpire: 브레이크 시간 ( 단위: 분 ),
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러, 3:입력값 없음, 4: 업체 없음 )
    msg: 처리 결과 메세지,
    data: 수정된 업체 데이터
}
```

---
---

# 모듈 : shop_web

---

## 1. 업체 소개말 설정

> 업체의 `소개말`을 설정한다.

---

- PATH
> '/setBrief'

- METHOD
> POST

- PARAMETER
```
{
    chkKey: API요청 검증키,
    brief: 등록할 소개말
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: 결과 데이터 ( 업체 / 에러 )
}
```

---

## 2. 업체 메뉴 품절 설정

> 업체에서 제공하는 메뉴의 `품절` 상태를 설정한다.

---

- PATH
> '/setStock'

- METHOD
> POST

- PARAMETER
```
{
    id: 설정할 업체의 _id,
    soldout: 품절 여부,
    menu: 설정할 메뉴의 menuId,
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지
}
```

---

## 3. 업체 _id 조회

> 사업자 번호로 해당 업체의 `_id`를 조회한다.

---

- PATH
> '/getId/:bsNum'

- METHOD
> GET

- PARAMETER
```
bsNum: _id를 조회 할 업체의 사업자번호
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러, 3:입력값 없음 )    
    msg: 처리결과 메세지,
    data: 업체의 _id
}
```

---

# 모듈 : order

---

## 1. 주문 상세 내역 조회

> `주문`의 `상세 내역`을 조회한다.

---

- PATH
> '/detail/:orderId'

- METHOD
> GET

- PARAMETER
```
orderId : 조회할 주문의 _id
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: 결과 데이터 ( 업체 / 에러 )
}
```

---

## 2. 주문 상세 내역 조회

> `키워드 / 날짜`로 해당하는 `주문`들을 조회 한다.

---

- PATH
> '/search'

- METHOD
> POST

- PARAMETER
```
orderId : 조회할 주문의 _id
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: 결과 데이터 ( 업체 / 에러 )
}
```

---

## 3. 업체 최종 주문 등록시간 조회

> 업체에 가장 마지막으로 `주문이 등록된 시간`을 조회한다.

---

- PATH
> '/checkTimestamp/:bsNum'

- METHOD
> GET

- PARAMETER
```
bsNum : 사업자 번호
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: {
        lastOrderRegiTime: 최종 등록 시간 // 1598954024278
    }
}
```

---


## 4. 업체 주문 상태별 카운트

> 업체에 등록된 `주문의 수량`을 `상태별`로 조회

---

- PATH
> '/count/:bsNum'

- METHOD
> GET

- PARAMETER
```
bsNum : 사업자 번호
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: {
        ready: 접수 요청상태 주문의 수,
        wait: 수락하고 처리 중인 주문의 수,
        done: 서빙이 완료된 상태의 주문의 수,
        end: 서비스가 종료된 주문의 수,
        lastOrderRegiTime: 가장 마지막에 주문이 등록된 시각의 타임스탬프,
        /*
            "ready": 0,
            "wait": 0,
            "done": 0,
            "end": 4,
            "lastOrderRegiTime": 1598954024278        
        */
    }
}
```

---

## 5. 업체 주문 상태별 카운트

> 업체에 등록된 `주문의 수량`을 `상태별`로 조회

---

- PATH
> '/count/:bsNum'

- METHOD
> GET

- PARAMETER
```
bsNum : 사업자 번호
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: {
        ready: 접수 요청상태 주문의 수,
        wait: 수락하고 처리 중인 주문의 수,
        done: 서빙이 완료된 상태의 주문의 수,
        end: 서비스가 종료된 주문의 수,
        lastOrderRegiTime: 가장 마지막에 주문이 등록된 시각의 타임스탬프,
        /*
            "ready": 0,
            "wait": 0,
            "done": 0,
            "end": 4,
            "lastOrderRegiTime": 1598954024278        
        */
    }
}
```

---

## 6. 업체 주문 내역 전체 조회 ( 전체시간 )

> 업체에 등록된 `주문 내역 전체`를 조회

---

- PATH
> '/list/allTime/:bsNum'

- METHOD
> GET

- PARAMETER
```
bsNum : 사업자 번호
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: 조회 요청 결과
    // [ 주문객체1, 주문객체2 ]
}
```

---

## 7. 업체 주문 내역 전체 조회 ( 특정 시간 범위, getRangeTime )

> 업체에 등록된 해당 시간 범위 안의 `주문 내역 전체`를 조회

---

- PATH
> '/list/all/:bsNum'

- METHOD
> GET

- PARAMETER
```
bsNum : 사업자 번호
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: 조회 요청 결과
    // [ 주문객체1, 주문객체2 ]
}
```

---

## 8. 업체 접수대기 주문 내역 조회 ( 특정 시간 범위, getRangeTime )

> 업체에 등록된 해당 시간 범위 안의 `접수대기 상태의 주문 내역 전체`를 조회

---

- PATH
> '/list/ready/:bsNum'

- METHOD
> GET

- PARAMETER
```
bsNum : 사업자 번호
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: 조회 요청 결과
    // [ 주문객체1, 주문객체2 ]
}
```

---


## 9. 업체 처리중인 주문 내역 조회 ( 특정 시간 범위, getRangeTime )

> 업체에 등록된 해당 시간 범위 안의 `처리중 상태의 주문 내역 전체`를 조회

---

- PATH
> '/list/ready/:bsNum'

- METHOD
> GET

- PARAMETER
```
bsNum : 사업자 번호
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: 조회 요청 결과
    // [ 주문객체1, 주문객체2 ]
}
```

---

## 10. 업체 서빙 완료 주문 내역 조회 ( 특정 시간 범위, getRangeTime )

> 업체에 등록된 해당 시간 범위 안의 `서빙 완료된 주문 내역 전체`를 조회

---

- PATH
> '/list/done/:bsNum'

- METHOD
> GET

- PARAMETER
```
bsNum : 사업자 번호
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: 조회 요청 결과
    // [ 주문객체1, 주문객체2 ]
}
```

---

## 11. 업체 서비스 종료된 주문 내역 조회 ( 특정 시간 범위, getRangeTime )

> 업체에 등록된 해당 시간 범위 안의 `서비스가 종료된 주문 내역 전체`를 조회

---

- PATH
> '/list/end/:bsNum'

- METHOD
> GET

- PARAMETER
```
bsNum : 사업자 번호
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: 조회 요청 결과
    // [ 주문객체1, 주문객체2 ]
}
```

---


## 12. 업체 주문 접수 거절

> 업체에 접수된 `주문을 거절하고` 결제대금 `환불` 처리

---

- PATH
> '/reject'

- METHOD
> POST

- PARAMETER
```
{
    orderId : 주문의 _id,
    reason : 취소 사유
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: [취소 처리된 주문객체]
}
```

---

## 13. 업체 주문 확인

> 업체에 접수된 `주문 요청을 확인`

---

- PATH
> '/check'

- METHOD
> POST

- PARAMETER
```
{
    orderId : 주문의 _id,
    time : 예상 처리 시간 ( 단위 : 분 )
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: [확인한 주문객체]
}
```

---

## 14. 업체 주문 처리 완료

> 업체에 접수된 `주문의 처리 완료`

---

- PATH
> '/done'

- METHOD
> POST

- PARAMETER
```
{
    orderId : 주문의 _id,
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: [처리완료된 주문객체]
}
```

---


## 15. 업체 주문 서비스 종료

> 업체에 주문 접수한 테이블의 `서비스 종료`

---

- PATH
> '/end'

- METHOD
> POST

- PARAMETER
```
{
    orderId : 주문의 _id,
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: [서비스 종료된 주문객체]
}
```

---


## 16. 업체 주문 환불

> 업체에 등록된 주문을 접수, 처리, 서비스, 등록일자에 관계없이 `환불 및 취소 처리`

---

- PATH
> '/refund'

- METHOD
> POST

- PARAMETER
```
{
    orderId : 주문의 _id,
    reason : 환불 사유
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: [환불된 주문객체]
}
```

---

# 모듈 : test

---

## 1. 최종 주문 등록 시간 갱신

> `업체`의 `최종 주문 등록시간`을 `현재 시각`으로 갱신한다.

---

- PATH
> '/renewOrderRegiTime/:bsNum'

- METHOD
> GET

- PARAMETER
```
bsNum : 사업자 번호
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: {
        lastOrderRegiTime: 최종 주문 등록시간
    }
}

/*
    {
        "result": 1,
        "msg": "ok",
        "data": {
            "lastOrderRegiTime": 1599115544683
        }
    }
*/
```

---


## 2. 업체 테이블 상태 변경

> `업체`의 `테이블 점유 상태`를 설정한다.

---

- PATH
> '/setTableVacancy'

- METHOD
> POST

- PARAMETER
```
{
    shopId: 업체 _id,
    tableName: 테이블 명,
    tableVacancy: 설정할 점유상태,
    ( true: 사용가능, false: 사용불가)
}
```

- RETURN
```
{
    result: 응답코드,
    ( 1:성공, 2:에러 )    
    msg: 처리결과 메세지,
    data: {
        _id: 업체 _id,
        shopName: 업체명,
        tables: [{
            _id: 테이블 _id,
            tableName: 테이블 명,
            tableSize: 테이블 가용 인원,
            tableVacancy: 테이블 점유 상태
        },...,{}]
    }
}

/*
    {
        "result": 1,
        "msg": "save well",
        "data": {
            "_id": "5c667f2e60800a0c92293357",
            "shopName": "칼로리 스테이션",
            "tables": [
                {
                    "_id": "5d5e226e4d7cc309bcfcbc74",
                    "tableName": "1",
                    "tableSize": "4",
                    "tableVacancy": true
                },
            ]
        }
    }
*/
```
---

