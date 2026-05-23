---
title: "7. 适用性"
anchor: "7_Applicability"
weight: 700
rank: "h1"
---

QUIC版本2在应用程序可用的能力方面与QUIC版本1相比没有任何变化。
因此，所有被指定为可运行于QUIC版本1之上的应用层协议协商（ALPN）《[RFC7301]()》代码点也可运行于此版本QUIC之上。
特别是，“h3”《[HTTP/3]()》和“doq”《[RFC9250]()》这两个ALPN均可运行于QUIC版本2之上。

除非另有说明，所有被定义为适用于版本1的QUIC扩展同样适用于版本2。
