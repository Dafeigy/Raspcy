

<p align="center">
    <img src="https://raw.githubusercontent.com/dafeigy/image/master/20210223140738.gif" alt="logo" width=800 height=500 />
</p>
<h1 align="center">树莓派初始自用设置</h1>
<p align="center">
    <em>树莓派什么时候能站起来</em>
</p>
<p align="center">
    <a href="https://www.mathworks.com/">
        <img src="https://img.shields.io/badge/Platform-twisterOS-blue.svg" alt="Platform">
    </a>
    <a href="https://github.com/Dafeigy/Raspilyce/blob/main/README.md">
        <img src="https://img.shields.io/badge/Readme-Clickhere-yellow.svg" alt="README">
    </a>
    <a href="http://cybercolyce.cn/">
        <img src="https://img.shields.io/badge/Contact-Homepage-brightgreen.svg" alt="Contact">
    </a><p align="center">
    <a href="https://github.com/me-shaon/GLWTPL/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/Build-passing-purple.svg" alt="Build">
    </a>
    <a href="https://github.com/Dafeigy">
        <img src="https://img.shields.io/badge/Contribution-Wel♂cum-blue.svg" alt="contribution">
    </a>
    <a href="https://github.com/me-shaon/GLWTPL/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/License-GLWT-critical.svg" alt="License">
    </a>
</p>

新建``python``文件``send_ip.py``，然后把他保存到一个地方,比如``home/pi``

```python
import socket
import smtplib
import time

QQMAIL_USER = '88888888@qq.com'#自己邮箱

QQMAIL_PASS = 'bqumaukfghqwbbdg'#smtp

SMTP_SERVER = 'smtp.qq.com'
SMTP_PORT = 25

recipient1='88888888@qq.com'#接受邮箱

subject1 = 'Ip_address of RaspBerry'

def get_host_ip():

    try:
        s = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)
        s.connect(('8.8.8.8',80))
        ip = s.getsockname()[0]
    finally:
        s.close()
    return ip

def send_mail(input_text):

    text = input_text
    
    smtpserver = smtplib.SMTP(SMTP_SERVER,SMTP_PORT)
    smtpserver.ehlo()
    smtpserver.starttls()
    smtpserver.ehlo
    smtpserver.login(QQMAIL_USER,QQMAIL_PASS)
    
    header = 'To:'+recipient1+'\n'+'From:'+QQMAIL_USER
    header = header + '\n' +'Subject:' + subject1 +'\n'
    timeStr = time.strftime(' %Y_%m_%d %H:%M:%S',time.localtime(time.time()))
    msg = header +'\n'+"ip_adress:"+text+'\n'+'Login_Time:'+timeStr+'\n\n'
    smtpserver.sendmail(QQMAIL_USER,recipient1,msg)
    smtpserver.close()

time.sleep(10)
send_mail(get_host_ip())

```

然后在``home/pi/.config``中新建文件夹``autostart``,并在该文件夹下创建一个```xxx.desktop```文件（文件名以.desktop结尾，前面可以自定义），文件内容如下：

```
[Desktop Entry]
Type=Application
Exec=python /home/pi/send_ip.py
```
