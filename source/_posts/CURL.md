title: CURL
author: MiracleQi-温柔魔君
tags:
  - command
  - curl
categories:
  - Linux
date: 2016-06-22 16:21:00
cover: /img/post-cover/23.jpg
---
curl 参考手册及示例

# 前言

curl 是很方便的 Rest 客戶端，可以很方便的完成許多 Rest API 測試的需求，甚至，如果是需要先登入或認證的 rest api，也可以進行測試，利用 curl 指令，可以送出 HTTP GET, POST, PUT, DELETE, 也可以改變 HTTP header 來滿足使用 REST API 需要的特定條件。

# 常用参数

curl 的參數很多，這邊僅列出目前測試 REST 時常用到的:

```
-X/--request [GET|POST|PUT|DELETE|…] 使用指定的 http method 發出 http request
-H/--header 設定request裡的header
-i/--include 顯示response的header
-d/--data 設定 http parameters
-v/--verbose 輸出比較多的訊息
-u/--user 使用者帳號、密碼-b/--cookie cookie
```

# 示例

## -X http method

GET/POST/PUT/DELETE使用方式  
-X 後面加 http method
```
curl -X GET "http://www.rest.com/api/users"
curl -X POST "http://www.rest.com/api/users"
curl -X PUT "http://www.rest.com/api/users"
curl -X DELETE "http://www.rest.com/api/users"
```
url要加引號也可以，不加引號也可以，如果有非純英文字或數字外的字元，不加引號可能會有問題，如果是網碼過的 url，也要加上引號

## -H 自定义请求头

HEADER  
在 http header 加入的訊息
```
curl -v -i -H "Content-Type: application/json" http://www.example.com/users
```

## -d data

HTTP Parameter  
http 參數可以直接加在 url 的 query string，也可以用 -d

帶入參數間用 & 串接，或使用多個 -d

```
# 使用`&`串接多個參數
curl -X POST -d "param1=value1&param2=value2"
# 也可使用多個`-d`，效果同上
curl -X POST -d "param1=value1" -d "param2=value2"
curl -X POST -d "param1=a 0space"
# "a space" url encode 後空白字元會編碼成 ' ' 為 "a space"，編碼後的參數可以直接使用
curl -X POST -d "param1=a space"
```
post json 格式得資料  
如同時需要傳送 request parameter 跟 json，request parameter 可以加在 url 後面，json 資料則放入 -d 的參數，然後利用單引號將 json 資料含起來(如果 json 內容是用單引號，-d 的參數則改用雙引號包覆)，header 要加入 ”Content-Type:application/json”跟 ”Accept:application/json”
```
curl http://www.example.com?modifier=kent -X PUT -i -H "Content-Type:application/json" -H "Accept:application/json" -d '{"boolean" : false, "foo" : "bar"}'
# 不加"Accept:application/json"也可以
curl http://www.example.com?modifier=kent -X PUT -i -H "Content-Type:application/json" -d '{"boolean" : false, "foo" : "bar"}'
```

## 认证

需先認證或登入才能使用的service  
許多服務，需先進行登入或認證後，才能存取其 API 服務，依服務要求的條件，的curl 可以透過 cookie，session 或加入在 header 加入 session key，api key 或認證的 token 來達到認證的效果。

### session

後端如果是用 session 記錄使用者登入資訊，後端會傳一個 session id 給前端，前端需要在每次跟後端的 requests 的 header 中置入此 session id，後端便會以此 session id 識別前端是屬於那個 session，以達到 session 的效果
```
curl --request GET 'http://www.rest.com/api/users'--header 'sessionid:1234567890987654321'
```
### cookie

如果是使用 cookie，在認證後，後端會回一個 cookie 回來，把該 cookie 成檔案，當要存取需要任務的 url 時，再用 -b cookie_file 的方式在 request 中植入 cookie 即可正常使用

```
# 將cookie存檔
curl -i -X POST -d username=kent -d password=kent123 -c ~/cookie.txt http://www.rest.com/auth
# 載入cookie到request中
curl -i --header "Accept:application/json" -X GET -b ~/cookie.txt http://www.rest.com/users/1
```

## 檔案上傳

```
curl -i -X POST -F 'file=@/Users/kent/my_file.txt' -F 'name=a_file_name'
```

這個是透過 HTTP multipart POST 上傳資料，```-F``` 是使用 http query parameter 的方式，指定檔案位置的參數要加上 ```@```

## Basic Authentication
HTTP Basic Authentication (HTTP基本認證)  
如果網站是採HTTP基本認證, 可以使用 ```--user username:password``` 登入
```
curl -i --user kent:secret http://www.rest.com/api/foo'
```
認證失敗時，會是 401 Unauthorized
```
HTTP/1.1 401 Unauthorized
Server: Apache-Coyote/1.1
X-Content-Type-Options: nosniff
X-XSS-Protection: 1; mode=block
Cache-Control: no-cache, no-store, max-age=0, must-revalidate
Pragma: no-cache
Expires: 0
X-Frame-Options: DENY
WWW-Authenticate: Basic realm="Realm"
Content-Type: text/html;charset=utf-8
Content-Language: en
Content-Length: 1022
Date: Thu, 15 May 2014 06:32:49 GMT
```
認證通過時，會回應 200 OK
```
HTTP/1.1200 OK
Server:Apache-Coyote/1.1
X-Content-Type-Options: nosniff
X-XSS-Protection:1; mode=block
Cache-Control:no-cache,no-store, max-age=0, must-revalidate
Pragma:no-cache
Expires:0
X-Frame-Options: DENY
Set-Cookie: JSESSIONID=A75066DCC816CE31D8F69255DEB6C30B;Path=/mdserver/;HttpOnly
Content-Type: application/json;charset=UTF-8
Transfer-Encoding: chunked
Date:Thu,15May201406:14:11 GMT
```
可以把認證後的cookie存起來，重複使用
```
curl -i --user kent:secret http://www.rest.com/api/foo' -c ~/cookies.txt
```
登入之前暫存的cookies，可以不用每次都認證
```
curl -i http://www.rest.com/api/foo' -b ~/cookies.txt
```