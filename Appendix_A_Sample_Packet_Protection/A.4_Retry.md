---
title: "重试"
anchor: "A.4_Retry"
weight: 1140
rank: "h2"
---

本附录展示了一个可能响应[附录A.2](#A.2_Client_Initial)中的Initial数据包而发送的Retry数据包。
完整性检查包含客户端选择的连接ID值`0x8394c8f03e515708`，但该值不包含在最终的Retry数据包中：
```
cf6b3343cf0008f067a5502a4262b574 6f6b656ec8646ce8bfe33952d9555436
65dcc7b6
```