---
page-title: "jck28 - 小柒 - 接口自动化测试L2 请求构造与响应断言 - 学习笔记 - 测试人社区"
url: https://ceshiren.com/t/topic/29762
date: "2024-04-23 13:42:22"
---
## [](https://ceshiren.com/t/topic/29762#h-1)一，接口请求体 - 文件上传

## [](https://ceshiren.com/t/topic/29762#h-11-2)1.1 文件上传

-   `Content-Type` 类型： `multipart/form-data`

[![[附件/f35e49d921eb66e5823fbf6d42c73ac9_MD5.png]]](https://ceshiren.com/uploads/default/original/3X/1/9/197cb098d3300aa1d0210ad9a33068f6172e4fe8.png "image")

-   上传文件内容  
    
    [![[附件/2a9e3d6a5120772faaacc865ef190529_MD5.png]]](https://ceshiren.com/uploads/default/original/3X/c/d/cddcfc6e2897cb1158e31d4ed53d175db7c40958.png "image")
    
-   调用方法multiPart()
    
    -   参数：`String name`
    -   参数：`File file`

```
package multiPart;

import io.restassured.RestAssured;
import io.restassured.specification.ProxySpecification;
import org.junit.jupiter.api.Test;

import java.io.File;

import static io.restassured.RestAssured.given;
import static io.restassured.specification.ProxySpecification.host;

public class multiPartTest {
    @Test
    void testUplaodFile(){
        // 需要上传的文件对象
        File myFile = new File("src/test/resources/request.txt");
        // 定义一个代理的配置信息
        RestAssured.proxy= host("localhost").withPort(8888);
        // 忽略HTTPS校验
        RestAssured.useRelaxedHTTPSValidation();

        given()
                .multiPart("apiTest", myFile)        // 传递文件对象
                .multiPart("ceshiren","{\\\"hogwarts\\\": 666}","application/json")      // 传递JSON数据
                .log().headers()
                .log().body()
        .when()
                .post("http://10.177.119.13:25201/v1/mixapi/ad_list")
        .then()
                .statusCode(200)
                .log().all();
    }

}

```

## [](https://ceshiren.com/t/topic/29762#h-12-form-3)1.2 form表单请求

-   应用场景
    
    -   数据量不大
    -   数据层级不深的情况
    -   通常以键值对传递
-   数据类型
    
    -   application/x-www-form-urlencoded  
        ![[附件/bd4ef30c9c09064e81f23691bc515789_MD5.png]]
-   调用方法： `formParam()`
    

```
package multiPart;

import io.restassured.RestAssured;
import org.junit.jupiter.api.Test;
import static io.restassured.RestAssured.given;
import static io.restassured.specification.ProxySpecification.host;

public class formTest {
    @Test
    void testFormParam(){
        // 配置本地代理，方便监听请求信息
        RestAssured.proxy= host("localhost").withPort(8888);
        // 忽略HTTPS校验
        RestAssured.useRelaxedHTTPSValidation();

        given()
                .formParam("myParam","hogwarts")      // 添加表单数据
                .log().all()
        .when()
                .post("http://10.177.119.13:25201/v1/mixapi/ad_list")
        .then()
                .statusCode(200)
                .log().all();
    }

    @Test
    void testFormParams(){
        // 配置本地代理，方便监听请求信息
        RestAssured.proxy= host("localhost").withPort(8888);
        // 忽略HTTPS校验
        RestAssured.useRelaxedHTTPSValidation();

        given()
                .formParams("username","hogwarts","password","demi623")      // 添加表单数据
                .log().all()
                .when()
                .post("http://10.177.119.13:25201/v1/mixapi/ad_list")
                .then()
                .statusCode(200)
                .log().all();
    }
}

```

## [](https://ceshiren.com/t/topic/29762#h-13-jsonxml-4)1.3 json/xml请求

### [](https://ceshiren.com/t/topic/29762#h-131-json-5)1.3.1 json请求示例

```
package multiPart;

import org.junit.jupiter.api.Test;
import static io.restassured.RestAssured.given;

public class jsonTest {
    @Test
    void jsonParam(){
        String jsonStr = "{\n" +
                "    \\\"data\\\": {\n" +
                "        \\\"ext\\\": {\n" +
                "            \\\"keyword\\\": \\\"腾讯视频\\\",\n" +
                "            \\\"supportMarketDetail\\\": \\\"true\\\"\n" +
                "        },\n" +
                "        \\\"posIds\\\": [\n" +
                "            \\\"18620_18687_49558_49564\\\"\n" +
                "        ],\n" +
                "        \\\"enterId\\\": \\\"3\\\",\n" +
                "        \\\"moduleId\\\": \\\"25\\\"\n" +
                "    },\n" +
                "    \\\"header\\\": {\n" +
                "        \\\"h\\\": 2340,\n" +
                "        \\\"w\\\": 1080,\n" +
                "        \\\"ua\\\": \\\"\\\",\n" +
                "        \\\"vn\\\": \\\"100\\\",\n" +
                "        \\\"mac\\\": \\\"02:00:00:00:00:00\\\",\n" +
                "        \\\"net\\\": \\\"wifi\\\",\n" +
                "        \\\"ori\\\": 0,\n" +
                "        \\\"anId\\\": \\\"b01ee613484611ca\\\",\n" +
                "        \\\"duId\\\": \\\"F0A06CB2A18F4B148928BF22F4993DDC\\\",\n" +
                "        \\\"guId\\\": \\\"brwsy6vreh6t7y568i76\\\",\n" +
                "        \\\"imei\\\": \\\"866781059887172\\\",\n" +
                "        \\\"lang\\\": \\\"zh\\\",\n" +
                "        \\\"make\\\": \\\"OPPO\\\",\n" +
                "        \\\"ouId\\\": \\\"A8B0FD6DC91C4FC195B61261002776CBf3605797aedcbfb242cefa257ca00252\\\",\n" +
                "        \\\"appId\\\": \\\"\\\",\n" +
                "        \\\"model\\\": \\\"PCLM10\\\",\n" +
                "        \\\"ssoId\\\": \\\"\\\",\n" +
                "        \\\"region\\\": \\\"CN\\\",\n" +
                "        \\\"carrier\\\": \\\"\\\",\n" +
                "        \\\"channel\\\": \\\"2101\\\",\n" +
                "        \\\"pkgName\\\": \\\"\\\",\n" +
                "        \\\"scenesId\\\": 25,\n" +
                "        \\\"systemId\\\": \\\"MIX_8792\\\",\n" +
                "        \\\"linkSpeed\\\": 173,\n" +
                "        \\\"osVersion\\\": \\\"V5.2.1\\\",\n" +
                "        \\\"apiVersion\\\": \\\"9.0\\\",\n" +
                "        \\\"appStoreVc\\\": 7202,\n" +
                "        \\\"appStoreVn\\\": \\\"8.2.0\\\",\n" +
                "        \\\"clientTime\\\": 1564392920485,\n" +
                "        \\\"romVersion\\\": \\\"PACM00_11_A.29\\\",\n" +
                "        \\\"versionCode\\\": 90380,\n" +
                "        \\\"versionName\\\": \\\"8600\\\",\n" +
                "        \\\"classifyByAge\\\": \\\"TEEN\\\",\n" +
                "        \\\"androidVersion\\\": \\\"8.1.0\\\",\n" +
                "        \\\"instantVersion\\\": \\\"104504%2F1045%2F1\\\"\n" +
                "    }\n" +
                "}";
        given()
                .contentType("application/json")
                .body(jsonStr)
                .log().all()
        .when()
                .post("http://10.177.119.13:25201/v1/mixapi/ad_list")
        .then()
                .statusCode(200)
                .log().all();

    }
}

```

### [](https://ceshiren.com/t/topic/29762#h-132-xml-6)1.3.2 xml 接口请求和响应断言

-   通过xPath进行断言
    -   xPath是 XML 路径语言，是 XML Path Language 的缩写，用来确定 XML 文档中某部分位置
        
    -   xPath语法：  
        
        [![[附件/9000c4f8ef3185104901227987cde8bc_MD5.jpg]]](https://ceshiren.com/uploads/default/original/3X/3/7/3722fe0eacd2ce85f3bcbb14777359f9b7ea656d.jpeg "image")
        
    -   xml响应断言示例：
        

```
package multiPart;

import org.apache.commons.io.IOUtils;
import org.junit.jupiter.api.Test;
import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import static io.restassured.RestAssured.given;

public class xmlTest {

    @Test
    void xmlReq() throws IOException {
        // 定义请求体数据：源自文件对象
        File file = new File("src/test/resources/add.xml");
        FileInputStream fis = new FileInputStream(file);
        String reqBody = IOUtils.toString(fis, "UTF-8");

        given()
                .contentType("text/xml")
                .body(reqBody)
                .log().all()
        .when()
                .post("http://dneonline.com//calculator.asmx")
        .then()
                .log().all()
                .statusCode(200)
                .body("//AddResult.text()", equalTo("2"));
    }
}

```

## [](https://ceshiren.com/t/topic/29762#h-14-headerscookie-7)1.4 Headers/Cookie 处理

```
package multiPart;

import io.restassured.RestAssured;
import org.junit.jupiter.api.Test;
import static io.restassured.RestAssured.given;
import static io.restassured.specification.ProxySpecification.host;

public class TestHeader {
    @Test
    void testSetHeader() {

        // 配置本地代理，方便监听请求信息
        RestAssured.proxy = host("localhost").withPort(8888);
        RestAssured.useRelaxedHTTPSValidation();

        given()
//                .header("User-Agent", "hogwarts","ceshiren")    // 设置请求头，支持设置多个值
//                .headers("username","demi","Cookie","my_cookie=aslarjle") // 设置请求头，支持多个配置参数
                .cookie("Cookie","sami")
                .relaxedHTTPSValidation()  // 忽略HTTPS校验
        .when()
                .get("https://httpbin.ceshiren.com/get")  // 发送请求
        .then()
                .log().all()  // 打印完整响应信息
                .statusCode(200);  // 响应断言
    }
}

```

## [](https://ceshiren.com/t/topic/29762#h-15-8)1.5 超时处理

```
package multiPart;

import io.restassured.RestAssured;
import io.restassured.config.HttpClientConfig;
import io.restassured.config.RestAssuredConfig;
import org.junit.jupiter.api.Test;
import static io.restassured.RestAssured.given;

public class TimeoutTest {
    @Test
    void timeoutSet(){

        RestAssured.baseURI="https://httpbin.ceshiren.com";

        // 自定义HttpClientConfig对象
        // 设置响应超时时长为3秒，单位是毫秒
        HttpClientConfig httpClientConfig = HttpClientConfig
                .httpClientConfig()
                .setParam("http.socket.timeout",3000);
        // 定义RestAssuredConfig对象
        // 传入自定义的HttpClientConfig对象
        RestAssuredConfig timeout = RestAssuredConfig.config().httpClient(httpClientConfig);

        given()
                .config(timeout)
                .relaxedHTTPSValidation()  // 忽略HTTPS校验
        .when()
                .get("/delay/10")  // 特定接口，延迟10秒响应
        .then()
                .log().all()  // 打印完整响应信息
                .statusCode(200);  // 响应断言
    }
}

```

## [](https://ceshiren.com/t/topic/29762#h-16-rest-assured-9)1.6 REST assured 使用 代理配置

-   开启代理工具监听请求
-   配置代理
    -   局部：通过 `proxy()` 方法
    -   全局：定义 `proxy` 对象

```
package multiPart;

import io.restassured.RestAssured;
import org.junit.jupiter.api.Test;
import static io.restassured.RestAssured.given;
import static io.restassured.specification.ProxySpecification.host;

public class testHTTPProxy {
    @Test
    void httpProxy(){
        // 第一种方法：定义一个代理的配置信息
        RestAssured.proxy = host("localhost").withPort(8888);
        // 第二种方法：通过proxy()方法设置
        given()
                .proxy("localhost",8888)  // 设置代理
                .relaxedHTTPSValidation()      // 请求https接口时，需要加上忽略HTTPS校验
        .when()
                .get("http://httpbin.org/get")  // 发送 HTTP请求
        .then()
                .log().all()  // 打印完整响应信息
                .statusCode(200);  // 响应断言
    }
}

```

## [](https://ceshiren.com/t/topic/29762#h-17-10)1.7 多层嵌套响应断言

### [](https://ceshiren.com/t/topic/29762#jsonpath-11)JSONPath 简介

-   在 JSON 数据中定位和提取特定信息的查询语言。
-   JSONPath 使用类似于 XPath 的语法，使用路径表达式从 JSON 数据中选择和提取数据。
-   相比于传统的提取方式，更加灵活，并且支持定制化。

### [](https://ceshiren.com/t/topic/29762#jsonpath-12)JSONPath 语法

[![[附件/4d40e881db166692be743ee4764194bd_MD5.jpg]]](https://ceshiren.com/uploads/default/original/3X/4/a/4a3547a69cf34c099c4d7598e4cd9a458d6407b4.jpeg "image")

### [](https://ceshiren.com/t/topic/29762#jsonpath-13)JSONPath 与代码结合

-   导入依赖

```
<!-- 相关依赖 -->
<properties>
    <json-path.version>2.8.0</json-path.version>
</properties>
<dependency>
      <groupId>com.jayway.jsonpath</groupId>
      <artifactId>json-path</artifactId>
      <version>${json-path.version}</version>
  </dependency>
```

-   测试演练环境地址  
    [https://jsonpath.hogwarts.ceshiren.com/](https://jsonpath.hogwarts.ceshiren.com/)
    
-   代码示例
    

```
package multiPart;

import com.jayway.jsonpath.DocumentContext;
import com.jayway.jsonpath.JsonPath;
import org.junit.jupiter.api.Test;
import java.util.ArrayList;
import static io.restassured.RestAssured.given;

public class jsonpathResTest {
    @Test
    void jsonpathRes(){
        String jsonData = "{\"username\":\"hogwarts\",\"password\":\"test12345\",\"code\":\"\"}";
        String res = given()
                .body(jsonData)
         .when()
                .post("https://httpbin.hogwarts.ceshiren.com/post")
         .then()
                .extract().response().getBody().asString();
        System.out.println(res);
        // 第一种获取方式
        DocumentContext context = JsonPath.parse(res);
        ArrayList<String> codeList = context.read("$..code");
        System.out.println(codeList);

        // 第二种获取方式
        String data = JsonPath.read(res, "$.data");
        System.out.println("data:" + data);
    }

}

```

## [](https://ceshiren.com/t/topic/29762#h-14)二，复杂断言与鉴权处理

## [](https://ceshiren.com/t/topic/29762#h-21-json-schema-15)2.1 JSON Schema

### [](https://ceshiren.com/t/topic/29762#h-16)简介

-   是使用 JSON 格式编写的
-   可以用来定义校验 JSON 数据的结构
-   可以用来校验 JSON 数据的一致性
-   可以用来校验 API 接口请求和响应

### [](https://ceshiren.com/t/topic/29762#json-schema-17)生成 JSON Schema 文档

-   JSON Schema 在线生成工具：[https://app.quicktype.io](https://app.quicktype.io/)
-   在线工具：[在线JSON数据生成JSON Schema](https://www.lddgo.net/string/generate-json-schema)

### [](https://ceshiren.com/t/topic/29762#json-schema-18)JSON Schema响应断言

-   导入依赖

```
<dependency>
    <groupId>io.rest-assured</groupId>
    <artifactId>json-schema-validator</artifactId>
    <version>4.4.0</version>
    <scope>test</scope>
</dependency>
```

-   代码示例
    -   将请求接口返回的响应结果生成对应的schema文件，然后存储在对应的schema.json文件
    -   代码断言schema文件

```
package multiPart;

import org.junit.jupiter.api.Test;
import static io.restassured.RestAssured.given;
import static io.restassured.module.jsv.JsonSchemaValidator.matchesJsonSchemaInClasspath;

public class TestJsonSchema {
    @Test
    void jsonSchemaTest() {

        given()
                .header("Hello", "Hogwarts")
        .when()
                .get("https://httpbin.ceshiren.com/get")  // 发送请求
        .then()
                .log().all()     // 打印完整的响应信息
                .assertThat()    //断言
                .body(matchesJsonSchemaInClasspath("schema.json"));  // JSON Schema 断言
    }
}

```

## [](https://ceshiren.com/t/topic/29762#h-22-19)2.2 数据库操作与断言

-   导入依赖

```
<dependency>
    <groupId>org.jooq</groupId>
    <artifactId>jooq</artifactId>
    <version>3.11.11</version>
</dependency>
<dependency>
    <groupId>com.jayway.jsonpath</groupId>
    <artifactId>json-path</artifactId>
    <version>2.6.0</version>
    <scope>test</scope>
</dependency>
<dependency>
      <groupId>mysql</groupId>
      <artifactId>mysql-connector-java</artifactId>
      <version>8.0.30</version>
</dependency>

```

-   封装数据库

```
package JDBC;

import org.jooq.Record;
import org.jooq.RecordMapper;
import org.jooq.impl.DSL;
import org.jooq.tools.json.JSONObject;
import java.sql.*;
import java.util.ArrayList;
import java.util.List;

public class DBUtil {
    Connection conn;
    Statement statement;

    //获取数据库连接对象
    public DBUtil(String sql, String username, String password){
        try {
            //连接数据库
            conn = DriverManager.getConnection(sql,username,password);
            //获取数据库操作对象（Statement专门执行sql语句，Statement接口不能接受参数）
            statement = conn.createStatement();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    // 根据 sql 返回在数据库查询的信息
    public List<Integer> getResultListBySQL(String sql_query, String columnLabel){
        List<Integer> resList = new ArrayList<>();
        try {
            ResultSet resultSet = statement.executeQuery(sql_query);
            while (resultSet.next()){
                resList.add(resultSet.getInt(columnLabel));
            }
        }catch (SQLException e) {
            e.printStackTrace();
        }
        return resList;
    }

    public String getJsonResultBySql(String sql_query){
        // 格式转换：将ResultSet转换为标准的json格式，方便完成断言。
        try {
            //获取结果集，executeQuery（）用于执行查询语句select，返回的是一个集合，将查询结果放在ResultSet类对象中供用户使用
            //int executeUpdate()用于执行INSERT,UPDATE,DELETE语句，返回受sql语句执行影响的行数
            ResultSet resultSet  = statement.executeQuery(sql_query);
            //ResultSetMetaData是用于分析结果集的元数据接口
            ResultSetMetaData metaData = resultSet.getMetaData();
            //获取数据表的列数
            int columnCount = metaData.getColumnCount();
            // 获取所有的数据表列名
            List<String> colNames = new ArrayList<>();
            for(int i=1;i<columnCount;i++){
                String name = metaData.getColumnName(i);
                colNames.add(name);
            }
            // 返回一个json结构的查询结果
            return DSL.using(conn)
                    .fetch(resultSet)
                    .map(new RecordMapper(){
                        @Override
                        public JSONObject map(Record r) {
                            JSONObject obj = new JSONObject();
                            colNames.forEach(cn -> obj.put(cn, r.get(cn)));
                            return obj;
                        }
                    }).toString();
        } catch (SQLException e) {
            e.printStackTrace();
        }
        // 如果异常，return 空 json，不影响后续逻辑执行
        return "{}";
    }


    //关闭资源
    /  **
     @param conn 连接对象
     @param stmt 数据库操作对象
     @param rs 结果集
     */
    public static void close(Connection conn, Statement stmt, ResultSet rs){
        if(stmt !=null){
            try{
                stmt.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if(rs !=null){
            try{
                rs.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if(conn !=null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

}

```

-   数据表断言

```
package JDBC;

import com.jayway.jsonpath.JsonPath;
import org.junit.jupiter.api.Test;
import java.util.List;

import static org.junit.jupiter.api.Assertions.*;

class DBUtilTest {
    //advert库
    final String url = "jdbc:mysql://10.52.46.16:33066/ads_communal";
    final String username = "mysql";
    final String password = "123456";
    String query = "select * from ads_ad_collect22 where deep_ocpc_type=41";


    @Test
    void getResultListBySQL() {
        DBUtil dbUtil = new DBUtil(url, username, password);
        List<Integer> adId= dbUtil.getResultListBySQL(query, "ad_id");
        System.out.println(adId);
        assertTrue(adId.contains(401087482));
    }

    @Test
    void getJsonResultBySql() {
        DBUtil dbUtil = new DBUtil(url, username, password);
        String res = dbUtil.getJsonResultBySql(query);
        System.out.println(res);
        List<Integer> finalRes = JsonPath.read(res,"$..ad_id");
        System.out.println(finalRes);
        assertTrue(finalRes.contains(401087478));
    }
}
```

## [](https://ceshiren.com/t/topic/29762#h-22-20)2.2 接口鉴权

### [](https://ceshiren.com/t/topic/29762#h-221-21)2.2.1 后端接口鉴权常用方法

-   cookie
    -   1.  携带身份信息请求认证
    -   2.  之后的每次请求都携带cookie信息，cookie记录在请求头中
-   token
    -   1.  携带身份信息请求认证
    -   2.  之后的每次请求都携带token认证信息
    -   3.  可能记录在请求头，可能记录在url参数中
-   auth
    -   每次请求携带用户的username和password，并对其信息加密
-   oauth2
    -   1.  携带身份信息请求认证
    -   2.  服务端向指定回调地址回传code
    -   3.  通过code获取token
    -   4.  之后的请求信息都携带token。
    -   典型产品 ：微信自动化测试

### [](https://ceshiren.com/t/topic/29762#h-222-cookie-22)2.2.2 cookie 鉴权

-   cookie获取
    -   1.  cookie 的获取（根据接口文档获取）
    -   2.  发送携带 cookie 的请求
        
        -   直接通过调用 cookie 方法
        -   通过在 filter 中添加 cookieFilter 对象

```
package Authration;

import io.restassured.RestAssured;
import io.restassured.filter.cookie.CookieFilter;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.Test;
import static io.restassured.RestAssured.given;
import static io.restassured.specification.ProxySpecification.host;

public class CookieTest {
    // 发起set cookie请求。服务端会返回set cookie
    String setUrl = "https://httpbin.ceshiren.com/cookies/set/user/ad";
    // 查看当前请求中的cookie信息
    String url = "https://httpbin.ceshiren.com/cookies";

    @BeforeAll
    static void setUpClass(){
        // 设置全局代理
        RestAssured.proxy = host("localhost").withPort(8888);
        // 设置全局忽略证书认证
        RestAssured.useRelaxedHTTPSValidation();
    }

    @Test
    void addCookie(){
        // 直接通过cookie方法，添加cookie
        given()
                .cookie("user","ad")
        .when().get(url)
        .then().log().all();
    }

    @Test
    void addCookieByFilter(){
        CookieFilter cookieFilter = new CookieFilter();
        // 第一次请求，不进行重定向
        given().filter(cookieFilter).log().all().redirects().follow(false)
        .when().get(setUrl)
        .then().log().all();
        // 第二次请求，会通过cookieFilter 自动添加 user=ad cookie
        given().filter(cookieFilter).log().all()
        .when().get(url)
        .then().log().all();
        // 第三次请求，会通过cookieFilter 自动添加 user=ad cookie
        given().filter(cookieFilter).cookie("pass","123").log().all()
                .when().get(url)
                .then().log().all();
    }
}

```

### [](https://ceshiren.com/t/topic/29762#h-223-token-23)2.2.3 token鉴权

```
package Authration;

import io.restassured.RestAssured;
import org.junit.jupiter.api.Test;
import static io.restassured.RestAssured.given;
import static io.restassured.specification.ProxySpecification.host;

public class TokenTest {
    @Test
    void tokenTest(){
        // 设置全局代理
        RestAssured.proxy = host("localhost").withPort(8888);
        // 设置全局忽略证书认证
        RestAssured.useRelaxedHTTPSValidation();
        // 登录的url
        String loginUrl = "https://litemall.hogwarts.ceshiren.com/admin/auth/login";
        // 查询货品的url
        String goodsListUrl = "https://litemall.hogwarts.ceshiren.com/admin/goods/list";
        String userData = "{\"username\": \"admin123\", \"password\": \"admin123\"}";
        // 登录之后获取token
        String token = given()
                .body(userData).contentType("application/json")
                .when().post(loginUrl)
                .then().log().all().extract().path("data.token");
        // 调用查询货品接口，必须添加token信息
        given()
                .header("X-Litemall-Admin-Token", token)
        .when().post(goodsListUrl)
        .then().log().all().statusCode(200);


    }
}

```

### [](https://ceshiren.com/t/topic/29762#h-224-auth-24)2.2.4 auth鉴权（了解）

-   在基本 HTTP 身份验证中，请求包含格式为 的标头字段Authorization: Basic
-   其中credentials是 ID 和密码的Base64编码，由单个冒号连接:。

```
package Authration;

import io.restassured.RestAssured;
import org.junit.jupiter.api.Test;

import static io.restassured.RestAssured.given;
import static io.restassured.specification.ProxySpecification.host;

public class AuthTest {
    @Test
    void auth(){
        // 定义一个代理的配置信息
        RestAssured.proxy = host("localhost").withPort(8888);
        // 忽略HTTPS校验
        RestAssured.useRelaxedHTTPSValidation();
        // 被测接口地址
        String authURL = "https://httpbin.ceshiren.com/basic-auth/hogwarts/123";
        given().log().all()
                .auth().basic("hogwarts", "123")  // 设置基本认证
        .when()
                .get(authURL)  // 发送GET请求
        .then().log().all().statusCode(200);
    }
}

```

## [](https://ceshiren.com/t/topic/29762#h-25)三，接口加解密

-   加密：明文转换成密文的过程
-   解密：密文还原成明文的过程
-   常见加密算法
    -   AES
    -   RSA
    -   MD5
    -   Base64

```
package Decode;

import org.apache.commons.codec.binary.Base64;
import org.junit.jupiter.api.Test;
import java.nio.charset.StandardCharsets;

public class Base64DecodeTest {
    @Test
    void testEnDecode(){
        String str="hogwarts";
        // 获取字节数组
        byte[] arr = str.getBytes(StandardCharsets.UTF_8);
        // 执行加密
        String encodeMsg = Base64.encodeBase64String(arr);
        System.out.println(encodeMsg);

        byte[] arr2 = Base64.decodeBase64("aG9nd2FydHM=");
        String decodeMsg = new String(arr2,StandardCharsets.UTF_8);
        System.out.println(decodeMsg);
    }
}

```

## [](https://ceshiren.com/t/topic/29762#h-26)四，多套被测环境

-   导入依赖

```
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.13.0</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-yaml</artifactId>
    <version>2.13.0</version>
</dependency>
```

-   在Resources文件夹新建一个yaml文件，从文件里获取对应的测试环境并进行切换

```
import com.fasterxml.jackson.core.type.TypeReference;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.dataformat.yaml.YAMLFactory;
import io.restassured.RestAssured;
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.Test;
import java.io.File;
import java.io.IOException;
import java.util.HashMap;

import static io.restassured.RestAssured.baseURI;
import static io.restassured.RestAssured.given;

public class TestEnvvYaml {
    @BeforeAll
     //使用Jackson读取yaml文件
    static void setupClass() throws IOException {
        // 实例化一个ObjectMapper 对象
        ObjectMapper objectMapper = new ObjectMapper(new YAMLFactory());
        // 读取 resources 目录中的envs.yaml文件
        ClassLoader classLoader = Thread.currentThread().getContextClassLoader();
        File yamlFile = new File(classLoader.getResource("envs.yaml").getFile());
        // 定义序列化的结构 TypeReference
        TypeReference<HashMap<String, String>> typeReference = new TypeReference<HashMap<String, String>>() {};
        // 解析envs.yaml文件内容
        HashMap<String, String> envs = objectMapper.readValue(yamlFile, typeReference);
        // 设置基路径，值为选定的域名地址
        RestAssured.baseURI = envs.get(envs.get("default"));
        System.out.println(baseURI);
    }

    @Test
    void testEnvs() {
        System.out.println(baseURI);
        //发起请求
        given()
        .when()
                .get("/get")
        .then()
                .statusCode(200);
    }
}

```

## [](https://ceshiren.com/t/topic/29762#h-27)五，多响应类型封装设计

-   应用场景：响应值不统一，导致断言比较困难的情况
-   解决方案：获得的响应信息全部转换为结构化的数据进行处理

### [](https://ceshiren.com/t/topic/29762#h-28)导入依赖

```
<!-- pom中的依赖 -->
<!-- 直接将xml转换成字符串json -->
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
    <version>2.13.1</version>
</dependency>
<dependency>
    <groupId>com.jayway.jsonpath</groupId>
    <artifactId>json-path</artifactId>
    <version>2.6.0</version>
    <scope>test</scope>
</dependency>
```

### [](https://ceshiren.com/t/topic/29762#h-29)代码示例

```
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.dataformat.xml.XmlMapper;
import com.jayway.jsonpath.JsonPath;
import org.junit.jupiter.api.Test;
import java.io.IOException;
import java.util.List;
import static io.restassured.RestAssured.given;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class XMLToJsonTest {
    //  xml 转换 json
    public String resToJsonConvert(String originRes) throws IOException {
        if(originRes.startsWith("<?xml")){
            XmlMapper xmlMapper = new XmlMapper();
            JsonNode jsonNode = xmlMapper.readTree(originRes.getBytes());
            ObjectMapper objectMapper = new ObjectMapper();
            originRes = objectMapper.writeValueAsString(jsonNode);
        }
        return originRes;
    }

    @Test
    void resToJson() throws IOException {
        String result = given()
                .when()
                .get("https://httpbin.ceshiren.com/get")
                .then()
                .extract().body().asString();
        List<String> host = JsonPath.read(result, "$..Host");
        assertEquals("httpbin.ceshiren.com", host.get(0));
    }

    @Test
    void xmlResToJson() throws IOException {
        String result = given()
                .when()
                .get("https://www.nasa.gov/rss/dyn/lg_image_of_the_day.rss")
                .then()
                .extract().body().asString();
        // 调用转换成json的方法
        String res = resToJsonConvert(result);
        System.out.println(res);
        List<String> title = JsonPath.read(res, "$..title");
        assertEquals("NASA Image of the Day", title.get(0));
    }

}

```