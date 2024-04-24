---
url: https://www.52pojie.cn/thread-1907503-1-2.html
---
```
from selenium import webdriver
import time
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.action_chains import ActionChains
driver = webdriver.Chrome()
option = webdriver.ChromeOptions()
option.add_experimental_option("detach", True)
# 忽略证书错误
option.add_argument('--ignore-certificate-errors')
# 忽略 Bluetooth: bluetooth_adapter_winrt.cc:1075 Getting Default Adapter failed. 错误
option.add_experimental_option('excludeSwitches', ['enable-automation'])
# 忽略 DevTools listening on ws://127.0.0.1... 提示
option.add_experimental_option('excludeSwitches', ['enable-logging'])
# 获取driver对象, 并将配置好的option传入进去 运行结束不关闭窗口
driver = webdriver.Chrome(options=option)
driver.get("https://www.zhipin.com/shenzhen/?sid=sem_pz_bdpc_dasou_title")
time.sleep(2)
#点击注册登陆
# driver.find_element(".user-nav .btns .btn-outline").click()
login = driver.find_element(By.XPATH, '/html/body/div[1]/div[1]/div[1]/div[4]/div/a').click()
bossType = input("手机号登录请输入1 微信登录请输入2:")
if bossType.isdigit():
    if bossType=='1':
        #输入登陆的手机号
        phone = input("请输入手机号")
        driver.find_element(By.XPATH,"./html/body/div/div/div[2]/div[2]/div[2]/div[1]/div[1]/div/span[2]/input").send_keys(phone)
        #获取验证码
        driver.find_element(By.XPATH,"/html/body/div/div/div[2]/div[2]/div[2]/div[1]/div[2]/div/span/div").click()
        time.sleep(5)
        # #点击完成验证
        driver.find_element(By.XPATH,"/html/body/div/div/div[2]/div/div[2]/div[1]/div[2]/div/span/div").click()
        time.sleep(3)
        #输入验证码
        yzm = input("请输入验证码")
        #输入验证码
        driver.find_element(By.XPATH,"/html/body/div/div/div[2]/div/div[2]/div[1]/div[2]/div/span/input").send_keys(yzm)
        #点击登协议 .login-policy-wrapper >  .agree-policy-wrapper
        driver.find_element(By.XPATH,"/html/body/div/div/div[2]/div[2]/div[2]/div[2]/span/input").click()
        #点击登陆
        driver.find_element(By.XPATH,"/html/body/div/div/div[2]/div[2]/div[2]/div[1]/div[3]/button").click()
        time.sleep(10)

    elif bossType=='2':
        driver.find_element(By.XPATH,"/html/body/div/div/div[2]/div[2]/div[2]/div[1]/div[4]/a").click()
        time.sleep(10)

else:
    print("请输入数字")       

# 打印当前路径

# 尝试直接跳转

# 判断元素是否存在
handles = driver.window_handles          #获取当前浏览器的所有窗口句柄
driver.switch_to.window(handles[-1]) 
driver.get("https://www.zhipin.com/web/geek/job-recommend")

# try:
time.sleep(2)
driver.window_handles
test_element = driver.find_element(By.XPATH,"/html/body/div[1]/div[1]/div/div/div[1]")
# print("判断元素是否存在")
# d点击经常投递的简历类型
driver.find_element(By.XPATH,"/html/body/div[1]/div[2]/div[1]/div/div[1]/a[3]/span").click()
# 获取职位列表
list_tab =driver.find_elements(By.XPATH,"/html/body/div[1]/div[2]/div[2]/div/div/div[1]/ul/li")

# 开始循环
while True:
    handles = driver.window_handles          #获取当前浏览器的所有窗口句柄
    driver.switch_to.window(handles[-1]) 
    list_tab[0].click()
    time.sleep(2)

    driver.find_element(By.LINK_TEXT,"立即沟通").click()
    # WebDriverWait(driver, 20).until(EC.new_window_is_opened(handles))
    wins = driver.window_handles
    print(wins)                             # 打印当前所有窗口的句柄
    print(driver.current_window_handle)     # 打印当前窗口的句柄
    # popup = driver.find_element(By.CSS_SELECTOR, '.greet-boss-dialog')
    # mask = driver.find_element(By.CSS_SELECTOR, '.greet-boss-dialog')
# 如果弹出div是不可见的，可以等待它变为可见
    # wait = WebDriverWait(driver, 10)
    # wait.until(EC.visibility_of_element_located((By.CSS_SELECTOR, '.greet-boss-dialog')))
    mask_element = WebDriverWait(driver, 10).until(
    EC.visibility_of_element_located((By.CSS_SELECTOR, '.greet-boss-dialog')))
    # 如果元素被找到并且是可见的，则遮罩层显示
    if mask_element:
        driver.find_element(By.XPATH,"/html/body/div[8]/div[2]/div[3]/a[2]").click()
        time.sleep(2)
        driver.get("https://www.zhipin.com/web/geek/job-recommend")
        time.sleep(2)
        handles = driver.window_handles          #获取当前浏览器的所有窗口句柄
        driver.switch_to.window(handles[-1]) 
        driver.find_element(By.XPATH,"/html/body/div[1]/div[2]/div[1]/div/div[1]/a[3]/span").click()
        # test_element = driver.find_element(By.XPATH,"/html/body/div[1]/div[1]/div/div/div[1]")
        # try:
        time.sleep(2)
        # driver.window_handles
        list_tab =driver.find_elements(By.XPATH,"/html/body/div[1]/div[2]/div[2]/div/div/div[1]/ul/li")
        time.sleep(2)

    else:
        print("遮罩层没有显示")

# except:
#     print('异常说明')

```