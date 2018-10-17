---
layout: post
title: "网络字节序与本机字节序"
subtitle: 'always use network byte order'
author: "S.D.X."
header-style: text
tags:
  - network
---

## 什么是字节序
简单说吧，字节序就是字节在内存中的放置顺序。对于二进制位长度超过8的数据来说，比如`uint32_t`类型的数字，占用了4个字节、32位，那么这4个字节在内存中该如何存放呢？

### 大端法·小端法
根据最高位字节存放的位置，字节序分为大端法(大端序)和小端法(小端序)。大端序是最高位字节存放在内存的低地址处，而小端序是最高位字节存放在内存的高地址处。
比如整数`89978`，十六进制为`0x15f7b`，按照大端序在内存中的摆放位置为`15f7b`，其中，最高位字节`0x01`放在内存的低地址处，按照小端序则相反为`7b5f01`，其中，最高位字节`0x01`放在内存的高地址处。

## 为啥会存在网络字节序
因为每个机器默认采用的方式不一样，为了保持数据在网络传输时一致，标准也特规定了网络字节序采用大端法。

## 网络字节序 · 本机字节序 · IP字符串之间的转换
- 本机字节序 &rarr; 网络字节序

**pyton**

```
import socket
socket.htonl(integer)  # Convert a 32-bit integer from host to network byte order.
socket.htons(integer)  # Convert a 16-bit integer from host to network byte order.
```

**c/c++**
```
#include <arpa/inet.h>

uint32_t htonl(uint32_t hostlong);  // converts the unsigned integer hostlong from host byte order to network byte order.
uint16_t htons(uint16_t hostshort);  // converts the unsigned short integer hostshort from host byte order to network byte order.
```

- 网络字节序 &rarr; 本机字节序

**python**
```
import socket
socket.ntohl(integer)  # Convert a 32-bit integer from network to host byte order.
socket.ntohs(integer)  # Convert a 16-bit integer from network to host byte order.
```

**c/c++**
```
#include <arpa/inet.h>

uint32_t ntohl(uint32_t netlong);  // converts the unsigned integer netlong from network byte order to host byte order.
uint16_t ntohs(uint16_t netshort);  // converts the unsigned short integer netshort from network byte order to host byte order.
```

- 网络字节序 &rarr; IP字符串

**python**
```
import socket
packed_ip = socket.inet_aton('192.168.1.1')
socket.inet_ntoa(packed_ip)
```

**c/c++**
```
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

char *inet_ntoa(struct in_addr in);
// converts the Internet host address in, given in network byte order, to a string in IPv4 dotted-decimal notation.
```

- 本机字节序 &rarr; IP字符串

本机字节序 &rarr; 网络字节序 &rarr; IP字符串

- IP字符串 &rarr; 网络字节序

**python**
```
import socket
socket.inet_aton('192.168.1.1')  # return 32-bit packed binary format used in low-level network functions.
```


**c/c++**
```
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

int inet_aton(const char *cp, struct in_addr *inp);
// converts the Internet host address cp from the IPv4 numbers-and-dots notation into binary form (in network byte order) and stores it in the structure that inp points to.
```

- IP字符串 &rarr; 本机字节序

IP字符串 &rarr; 网络字节序 &rarr; 本机字节序
