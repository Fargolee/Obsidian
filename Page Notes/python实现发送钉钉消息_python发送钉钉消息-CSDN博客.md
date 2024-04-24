---
page-title: "python实现发送钉钉消息_python发送钉钉消息-CSDN博客"
url: https://blog.csdn.net/weixin_43629644/article/details/127487985
date: "2024-04-24 18:46:43"
---
**需求：**企业部门本地部署的缺陷管理工具，企业内部使用[钉钉](https://so.csdn.net/so/search?q=%E9%92%89%E9%92%89&spm=1001.2101.3001.7020)进行工作交流，老板想让每天汇报项目的测试情况；

---

**设计思路：**

1、创建钉钉群机器人，每天发送项目测试信息（缺陷数量、关闭数量、修复数量、项目名称、新增缺陷数量、新增缺陷负责人）；

2、使用python读取mysql数据库的表 构造成钉钉的消息内容

实现方式：python3

---

一、安装[python开发环境](https://so.csdn.net/so/search?q=python%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83&spm=1001.2101.3001.7020)以及相关依赖库

安装python3开发环境可以百度；安装好后按下windowds+R，打开cmd，使用 pip install命令安装python库（需要库如下：pymysql，requests, json，nnlog)

二、创建本地文件夹DingMsg，并在文件夹 创建mysql.py和DingMsg.py

三、编写读取mysql的代码

```
import requests, jsonfrom pymysql import connectimport nnloglog = nnlog.Logger('DingMsg.log',level='debug',backCount=5,when='D')class Op_mysql:def __int__(self):print('aaaa')    @classmethoddef con_mysql(self,sql):        conn = connect(            host='',            port=,            user='',            password='',            db='',            charset='utf8')        cursor=conn.cursor()        cursor.execute(sql)        results = cursor.fetchone()for result in results:pass        log.info(result)        conn.close()return resultdef con_mysql_list(self, list):        conn = connect(            host='',            port=,            user='',            password='',            db='',            charset='utf8')        cursor = conn.cursor()        cursor.execute(list)        listname=[]        resultsList = cursor.fetchall()for r_List in resultsList:            listname.append(r_List)        log.info(listname)return listname    @classmethoddef getTodayNewbugs(self):        o = Op_mysql()        news=o.con_mysql(sql = "SELECT COUNT(*) FROM  WHERE DATEDIFF(,NOW())=0")return news    @classmethoddef getAllbugs(self):        o=Op_mysql()        all_bugs=o.con_mysql(sql="")return all_bugs    @classmethoddef getProjectname(self):        o=Op_mysql()        projectname = o.con_mysql_list(sql="")return projectname    @classmethoddef getassigned(self):        o = Op_mysql()        assigned = o.con_mysql_list(sql="")return assigned    @classmethoddef getWaitingBugs(self):        o = Op_mysql()        WaitingBugs=o.con_mysql(sql="")return WaitingBugs    @classmethoddef getClosebugs(self):        o = Op_mysql()        CloseBugs = o.con_mysql(sql="")return CloseBugs    @classmethoddef getFixbugs(self):        o = Op_mysql()        fixbugs = o.con_mysql(sql="")return fixbugsif __name__ == "__main__":    op_mysql=Op_mysql    op_mysql.getProjectname()    op_mysql.getAllbugs()    op_mysql.getWaitingBugs()    op_mysql.getClosebugs()    op_mysql.getassigned()
```

 四、编写DingMsg.py的代码

```
import requests, jsonfrom pymysql import connectimport mysqlfrom mysql import Op_mysqlimport nnloglog = nnlog.Logger('DingMsg.log',level='info',backCount=5,when='D')def send_dingtalk_message(url,content,mobile_list):    headers = {'Content-Type': 'application/json'}    data = {"msgtype": "text","text": {"content":content        },"at": {"atMobiles": mobile_list,"isAtAll": False        }    }    r = requests.post(url, headers=headers, data=json.dumps(data))    log.info(r.text)return r.textif __name__ == "__main__":    access_token = ''    op_mysql = Op_mysql    all_bugs = op_mysql.getAllbugs()    new_bugs = op_mysql.getTodayNewbugs()    projectname=op_mysql.getProjectname()    namelist=[]for name in projectname:for n in name:            namelist.append(n)if len(namelist)<=0:        namelist.append("中台")    log.info(namelist)    waitingbugs = op_mysql.getWaitingBugs()    fixbugs=op_mysql.getFixbugs()    closebugs=op_mysql.getClosebugs()    phonenumber_list = op_mysql.getassigned()    content = F"----测试日报----\n新增缺陷项目名称：{namelist}\n今日新增缺陷数：{new_bugs}\n今日关闭缺陷数：{closebugs}\n今日修复缺陷数：{fixbugs}\n待解决缺陷数：{waitingbugs}\n总缺陷数：{all_bugs}\n"    mobile_list = []for a in phonenumber_list:for b in a:            mobile_list.append(b)    log.info(mobile_list)try:if new_bugs >= 0:            send_dingtalk_message(access_token, content, mobile_list)except Exception as e:        log.error(e)
```

四、获取钉钉机器人的url

打开钉钉群，点击【群设置】-【智能群助手】添加机器人，选择自定义的机器人，选择自定义关键词，关键词填写 测试日报  。完成后将url填写到DingMsg.py的main方法的access\_token值上

![[附件/4f166bb7a315b74f9343747d4d54ebc9_MD5.png]]

 ![[附件/ab13af0c1b91255d51ab9a8f397d76be_MD5.png]] 五、执行DingMsg的main方法，验证消息能否发送成功

![[附件/aa79ba566c8e218cce5db33c593cd7df_MD5.png]]

六、在服务器上设置定时任务、定时执行脚本（crontal）

linux服务器定时任务编辑命令 crontab -e