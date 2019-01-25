---
title: Python网络入门
categories:
  - Python
tags:
  - 网络
reward: true
originContent: |-
  @[toc]

  ---

  # Python网络入门
  python的网络结构和C和C++的网络模型是一样的.

  ```Python
  from socket import *
  TCP: AF_INET SOCK_STREAM
      服务器模型:1.绑定地址和端口 2.监听 3.Accept 4.recv 5.send 6.close
      客户端模型:1.Connect 2.send 3.recv 4.close
  UDP: AF_INET SOCK_DGRAM
      服务器模型:1.bind 2.recvfrom 3.sendto 4.close
      客户端模型:1.sendto 2.recvfrom 3.close

  Python封装:
  from SocketServer import TCPServer as TCP, StreamRequestHandler as SRH 
      服务器模型:
      class MyRequestHandler(SRH):
          def handle(self):
              print '...connected from: ', self.client_address
              self.wfile.write('[%s] %s' % (ctime(), self.rfile.readline()))
      TCPServ = TCP(ADDR, MyRequestHandler)
      TCPServ.serve_forever()
      客户端模型:
  ```
toc: false
date: 2019-01-25 08:02:05
description:
---

@[toc]

---

# Python网络入门
python的网络结构和C和C++的网络模型是一样的.

```Python
from socket import *
TCP: AF_INET SOCK_STREAM
    服务器模型:1.绑定地址和端口 2.监听 3.Accept 4.recv 5.send 6.close
    客户端模型:1.Connect 2.send 3.recv 4.close
UDP: AF_INET SOCK_DGRAM
    服务器模型:1.bind 2.recvfrom 3.sendto 4.close
    客户端模型:1.sendto 2.recvfrom 3.close

Python封装:
from SocketServer import TCPServer as TCP, StreamRequestHandler as SRH 
    服务器模型:
    class MyRequestHandler(SRH):
        def handle(self):
            print '...connected from: ', self.client_address
            self.wfile.write('[%s] %s' % (ctime(), self.rfile.readline()))
    TCPServ = TCP(ADDR, MyRequestHandler)
    TCPServ.serve_forever()
    客户端模型:
```