# OData

* Retrieve
* Get x-csrf-token
* Create 
* Delete 

## Retrieve
- Basic Auth
- GET 외의 HTTP Method(POST, PUT, DELETE) 요청의 인증은 x-csrf-token 필요

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
