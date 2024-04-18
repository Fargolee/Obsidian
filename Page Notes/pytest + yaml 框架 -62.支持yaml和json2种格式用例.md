---
page-title: "pytest + yaml 框架 -62.支持yaml和json2种格式用例"
url: https://mp.weixin.qq.com/s/xwL8mRU0eEOEq4pFdyT0bw
date: "2024-04-18 20:07:30"
---
## 前言

v1.5.7版本开始新增json格式用例支持，本次版本改动内容

-   1.支持 .json 文件用例
    
-   2.优化日志中文件后缀名称.yml  .yaml .json
    
-   3.ruamel.yaml 版本兼容0.18.6
    

## yaml 格式用例

yaml 格式用例示例，test\_a.yml

```
test_demo:  name: post  request:    method: POST    url: http://httpbin.org/post    json:      username: test      password: "123456"  extract:      url:  body.url  validate:    - eq: [status_code, 200]    - eq: [headers.Server, gunicorn/19.9.0]    - eq: [$..username, test]    - eq: [body.json.username, test]
```

执行用例

```
pytest test_a.yml
```

## json 格式用例

前面的yaml 格式用例，等价于以下json格式用例，test\_x.json

```
{  "test_demo": {    "name": "post",    "request": {      "method": "POST",      "url": "http://httpbin.org/post",      "json": {        "username": "test",        "password": "123456"      }    },    "extract": {      "url": "body.url"    },    "validate": [      {"eq": ["status_code", 200]},      {"eq": ["headers.Server", "gunicorn/19.9.0"]},      {"eq": ["$..username", "test"]},      {"eq": ["body.json.username", "test"]}    ]  }}
```

执行用例

```
pytest test_x.json
```

运行报告日志

```
collected 1 item                                                                                                   
```

之前教程全是yaml格式用例，有部分同学反馈不太习惯yaml格式，所以新增了json格式的用例。