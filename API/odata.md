# OData

* CSRF
* Retrieve
* Get x-csrf-token
* Create 
* Delete 


## CSRF
CSRF (Cross-site request forgery) 사이트 간 요청 위조
 
사용자가 자신의 의지와 무관하게 공격자가 의도한 행동을 해서 특정 웹페이지를 보안에 취약하게 한다거나 수정, 삭제 등의 작업을 하게 만드는 공격 방법

이 공격으로부터의 예방은 사용자 세션 동안 보안 토큰을 유지하고 모든 수정 작업 (PUT, POST, DELETE)을 제공하는 것

제공된 토큰이 올바르지 않으면 게이트웨이는 403 Forbidden 상태로 응답

유효성은 설정 및 SAP_BASIS 릴리스에 따라 다르다.

[SAP Help Potal - CSRF Protection](https://help.sap.com/viewer/753088fc00704d0a80e7fbd6803c8adb/LATEST/en-US/5574ed6c93654ee4999b4d07cdda532c.html)

## Retrieve
- Basic Auth
- GET 외의 HTTP Method(POST, PUT, DELETE) 요청의 인증은 CSRF 토큰 필요

Request
```http
GET /sap/byd/odata/cust/v1/Service/EntitySet HTTP/1.1
Authorization: Basic {}
```

Response 
```xml
<?xml version="1.0" encoding="utf-8"?>
<feed xml:base="/sap/byd/odata/cust/v1/Service/" xmlns="http://www.w3.org/2005/Atom" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices">
    <id>/sap/byd/odata/cust/v1/Service/EntitySet</id>
    <title type="text">EntitySet</title>
    <updated>2021-06-21T06:35:44Z</updated>
    <author>
        <name/>
    </author>
    <link href="EDIErrorLogCollection" rel="self" title="EntitySet"/>
    <entry>
        <id>/sap/byd/odata/cust/v1/Service/EntitySet('00163EC0BE851EEBB4CA734BBB697AB1')</id>
        <content type="application/xml">
            <m:properties>
                <d:ObjectID>00163EC0BE851EEBB4CA734BBB697AB1</d:ObjectID>
            </m:properties>
        </content>
    </entry>
</feed>
```

## Get x-csrf-token
Request
```http
GET /sap/byd/odata/cust/v1/Service/EntitySet HTTP/1.1
x-csrf-token: fetch
```

Response 
```http
x-csrf-token: {token}
```

## Create
Request
```http
POST /sap/byd/odata/cust/v1/Service/EntitySet HTTP/1.1
x-csrf-token: {token}
```

## Delete
Request
```http
DELETE /sap/byd/odata/cust/v1/Service/EntitySet('00163EC0BE851EEBB4CA734BBB697AB1') HTTP/1.1
x-csrf-token: {token}
```


