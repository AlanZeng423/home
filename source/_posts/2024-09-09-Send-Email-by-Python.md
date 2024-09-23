---
layout: post
title: Send Email by Python
author: AlanZeng
date: 2024-09-09 11:12:30 -0800
tags: Development
---

# Send Email by Python
> 通过Python发送邮件

Key_points:

- SMTP服务器地址和端口
  - 使用TLS加密: 587
    ```python
    server = smtplib.SMTP(smtp_server, smtp_port)
    server.starttls()
    ```
  - 使用SSL加密: 465
    ```python
    server = smtplib.SMTP_SSL(smtp_server, smtp_port)
    ```


代码如下:
```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart

# 发送邮件
def send_email():
    print("Preparing to send email...")
    sender_email = 'your_email@example.com'
    receiver_email = 'receiver_email@example.com'
    password = 'your_email_password'

    smtp_server = 'smtp.yourmail.com'
    smtp_port = 587 # SMTP端口, 通常为587(TSL)或465(SSL)

    subject = 'subject'
    body = 'body'

    message = MIMEMultipart()
    message['From'] = sender_email
    message['To'] = receiver_email
    message['Subject'] = subject
    message.attach(MIMEText(body, 'plain'))

    try:
        print("Connecting to SMTP server...")
        # If you want to use SSL, use `smtplib.SMTP_SSL()` instead and remove `server.starttls()`
        with smtplib.SMTP(smtp_server, smtp_port) as server:
            server.starttls()  # 使用TLS加密
            print("Logging in to SMTP server...")
            server.login(sender_email, password)  # 登录
            print("Sending email...")
            server.sendmail(sender_email, receiver_email, message.as_string())  # 发送邮件
            print("Email sent successfully.")
    except Exception as e:
        print(f"Email sent failed: {e}")

# 主函数
def main():
    send_mail()
```