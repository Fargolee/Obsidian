---
page-title: "一秒钟学完所有Python内置模块"
url: https://mp.weixin.qq.com/s/IHpWXWz_YumiczDofgJfwA
date: "2024-04-18 20:06:27"
---
1.「sys」 - 用于访问与Python解释器相关变量和方法。  

`import sys   print(sys.argv)  # 打印命令行参数   `

2.「os」 - 提供与操作系统交互的功能。

`import os   print(os.getcwd())  # 打印当前工作目录   `

3.「re」 - 用于正则表达式操作。

`import re   match = re.search(r'\d+', 'There are 123 apples')   print(match.group())  # 打印匹配的数字   `

4.「math」 - 提供数学相关的函数。

`import math   print(math.sqrt(16))  # 打印16的平方根   `

5.「datetime」 - 用于处理日期和时间。

`from datetime import datetime   print(datetime.now())  # 打印当前日期和时间   `

6.「json」 - 用于处理JSON数据。

`import json   data = json.dumps({'name': 'Kimi', 'age': 5})   print(data)  # 将字典转换为JSON字符串   `

7.「collections」 - 提供有用的容器类型。

`from collections import defaultdict   d = defaultdict(lambda: 'N/A')   d['key'] = 'value'   print(d)  # 使用默认值的字典   `

8.「itertools」 - 提供创建迭代器的工具。

`import itertools   for pair in itertools.combinations('ABCD', 2):       print(pair)   `

9.「random」 - 提供生成随机数的功能。

`import random   print(random.randint(1, 10))  # 打印1到10之间的随机整数   `

10.「threading」 - 提供线程操作。

`import threading   def print_numbers():       for i in range(1, 6):           print(i)   t = threading.Thread(target=print_numbers)   t.start()   `

11.「queue」 - 提供线程安全的队列。

`from queue import Queue   q = Queue()   q.put('A')   q.put('B')   print(q.get())  # 安全地从队列中获取元素   `

12.「time」 - 提供时间相关的函数。

`import time   time.sleep(2)  # 暂停当前线程2秒   `

13.「urllib」 - 用于处理URL。

`from urllib.parse import urlparse   result = urlparse('http://www.example.com:80/path?query=value')   print(result.netloc)  # 打印URL的网络部分   `

14.「argparse」 - 用于命令行参数解析。

`import argparse   parser = argparse.ArgumentParser(description='Process some numbers.')   parser.add_argument('number', type=int, help='The input number')   args = parser.parse_args()   print(args.number)  # 解析命令行参数   `

15.「logging」 - 提供日志记录功能。

`import logging   logging.basicConfig(level=logging.INFO)   logging.info('This is an info message')   `

16.「shutil」 - 提供高级文件操作功能。

`import shutil   shutil.copy('source.txt', 'destination.txt')  # 复制文件   `

17.「hashlib」 - 提供哈希函数。

`import hashlib   m = hashlib.md5()   m.update(b'The quick brown fox jumps over the lazy dog')   print(m.hexdigest())  # 打印MD5哈希值   `

18.「pickle」 - 用于对象序列化。

`import pickle   data = {'key': 'value'}   pickle.dump(data, open('data.pkl', 'wb'))   # 将对象序列化到文件   `

19.「gzip」 - 用于读写gzip文件。

`import gzip   with gzip.open('file.txt.gz', 'wb') as f:       f.write(b'Some data to be compressed')   # 创建一个gzip压缩的文件   `

20.「tarfile」 - 用于读写tar文件。

`import tarfile   with tarfile.open('example.tar.gz', 'w:gz') as tar:       tar.add('example.txt')   # 创建一个gzip压缩的tar文件   `