# 淘宝万能抢单，有exe，有python源码，有讲解
Python完成淘宝抢单（非购物车）
购买分两步：第一步，点击立即购买；第二步，点击提交订单。

# 1.前期准备

操作系统：Windows
Python版本：3.7
谷歌浏览器

# 2.安装库

# 2.1 Selenium的安装
打开cmd，输入
pip install selenium

# 2.2ChromeDriver的安装
先确认使用的Chrome浏览器版本，在谷歌浏览器设置中可以找到，选择对应的版本进行下载，ChromeDriver的官方下载地址：
https://chromedriver.storage.googleapis.com/index.html
下载后解压至py文件目录下。

# 3.代码讲解

# 3.1运行浏览器
注意，地址中的‘/’，要用‘//’
browser = webdriver.Chrome("您的ChromeDriver地址")

# 3.2打开淘宝网站
代码如下：
browser.get("https://www.taobao.com")
# 3.3登录淘宝
代码如下：
browser.find_element_by_link_text("亲，请登录").click()
time.sleep(10)
随后，请在10s内用扫描二维码的方式登录，若是来不及，可将“10”改为更大的数字。

# 3.4输入目标商品的网址：
代码如下：
browser.get("目标商品的网址")

# 3.5一直尝试点击购买按钮
代码如下：
while True:
    # 点击购买按钮
    try:
        browser.find_element_by_id("J_LinkBuy").click()
        break
    except:
        print("时间未到")

# 3.6一直尝试提交订单
代码如下：
while True:
    try:
        browser.find_element_by_link_text('提交订单').click()
        print("抢购成功，请尽快付款")
    except:
        print("再次尝试提交订单")
        time.sleep(0.01)
最后就是付款环节了，可以松一口气。

# 4完整代码如下
from selenium import webdriver
import time
import datetime


# 打开Chrome浏览器
browser = webdriver.Chrome("C:\\Users\\86131\\Desktop\\唉\\chromedriver.exe")
browser.get("https://www.taobao.com")
# 扫码登陆
browser.find_element_by_link_text("亲，请登录").click()
time.sleep(10)

# 输入目标商品的网址,例如：
browser.get("https://detail.tmall.com/item.htm?id=629432524332&spm=a1z2k.11010449.931864.16.bd97509d96DF65&scm=1007.13982.82927.0&last_time=1603210511")

while True:
    # 点击购买按钮
    try:
        browser.find_element_by_id("J_LinkBuy").click()
        break
    except:
    	now = datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S.%f')
    	print(now)
        print("时间未到")

# 点击提交订单按钮
while True:
    try:
        browser.find_element_by_link_text('提交订单').click()
        print("抢购成功，请尽快付款")
        time.sleep(100000000000)
    except:
        print("再次尝试提交订单")
        time.sleep(0.01) # 若不满意，可改为0.001
