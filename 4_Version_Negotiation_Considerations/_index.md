---
title: "4. 版本协商考量"
anchor: "4_Version_Negotiation_Considerations"
weight: 400
rank: "h1"
---

QUIC版本2的目的并不是为了淘汰QUIC版本1。
支持QUIC版本2的终端可能继续支持版本1以最大限度兼容其他终端。
特别是，HTTP客户端通常使用Alt-Svc<sup>《[RFC7838]()》</sup>检测QUIC支持情况。
由于该机制目前还无法区分不同的QUIC版本，因此HTTP服务端{{< req_level SHOULD >}}支持多个QUIC版本，从而降低不兼容的概率以及由QUIC版本协商或TCP回退带来的开销。
例如，一个在Alt-Svc头部中表示支持“h3”的源站应该支持QUIC版本1，因为HTTP/3最初就是基于QUIC版本1的；因此，一些客户端只会支持该版本的QUIC。

任何支持QUIC版本2的QUIC终端{{< req_level MUST >}}发送、处理并验证《[QUIC VN]()》中定义的传输参数`version_information`，以防范版本降级攻击。

注意，版本2满足《[QUIC VN]()》中有关兼容QUIC版本1的定义，且QUIC版本1同样兼容版本2。
因此，服务端可以通过使用兼容版本协商在这两个版本之间切换连接。
同时支持这两个版本的终端{{< req_level SHOULD >}}支持兼容版本协商，从而避免一次往返。
