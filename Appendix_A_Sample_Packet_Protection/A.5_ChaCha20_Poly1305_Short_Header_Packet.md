---
title: "短头数据包示例"
anchor: "A.5_ChaCha20_Poly1305_Short_Header_Packet"
weight: 1150
rank: "h2"
---

本示例展示了使用短报头保护数据包所需的部分步骤。
它使用`AEAD_CHACHA20_POLY1305`算法。

在本示例中，TLS生成一个应用层写入密钥，服务器使用`HKDF-Expand-Label`和`SHA2-56`算法从该密钥派生四个值：一个密钥、一个初始化向量（IV）、一个报头保护密钥，以及密钥更新后将使用的密钥（本示例中不再使用最后一个值）。

```
secret
    = 9ac312a7f877468ebe69422748ad00a1
      5443f18203a07d6060f688f30f21632b

key = HKDF-Expand-Label(secret, "quicv2 key", "", 32)
    = 3bfcddd72bcf02541d7fa0dd1f5f9eee
      a817e09a6963a0e6c7df0f9a1bab90f2

iv  = HKDF-Expand-Label(secret, "quicv2 iv", "", 12)
    = a6b5bc6ab7dafce30ffff5dd

hp  = HKDF-Expand-Label(secret, "quicv2 hp", "", 32)
    = d659760d2ba434a226fd37b35c69e2da
      8211d10c4f12538787d65645d5d1b8e2

ku  = HKDF-Expand-Label(secret, "quicv2 ku", "", 32)
    = c69374c49e3d2a9466fa689e49d476db
      5d0dfbc87d32ceeaa6343fd0ae4c7d88
```

以下展示了使用空目标连接ID保护最小数据包所涉及的步骤。
该数据包包含一个PING帧（即仅为0x01的载荷），其数据包编号为654360564。在本示例中，使用长度为3的数据包编号（即编码为49140）可避免对数据包载荷进行填充；如果数据包编号使用更少的字节编码，则需要PADDING帧。

```
pn                 = 654360564 (decimal)
nonce              = a6b5bc6ab7dafce328ff4a29
unprotected header = 4200bff4
payload plaintext  = 01
payload ciphertext = 0ae7b6b932bc27d786f4bc2bb20f2162ba
```

生成的密文为可能的最小大小。
跳过一个字节以生成报头保护样本。

```
sample = e7b6b932bc27d786f4bc2bb20f2162ba
mask   = 97580e32bf
header = 5558b1c6
```

受保护的数据包是可能的最小数据包大小，为21字节。

```
packet = 5558b1c60ae7b6b932bc27d786f4bc2bb20f2162ba
```