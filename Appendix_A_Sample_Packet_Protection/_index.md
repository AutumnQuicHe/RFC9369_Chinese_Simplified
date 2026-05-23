---
title: "样本包保护示例"
anchor: "Appendix_A_Sample_Packet_Protection"
weight: 1100
rank: "h1"
---

本附录展示了数据包保护的示例，以便实现者能够逐步验证其实现。
文中定义了来自客户端和服务器的Initial数据包样本，以及一个Retry数据包样本。
这些数据包使用一个由客户端选择的8字节目标连接ID，其值为`0x8394c8f03e515708`。
文中还包含了一些中间值。
所有值均以十六进制表示。
