---
title: "密钥"
anchor: "A.1_keys"
weight: 1110
rank: "h2"
---

在`HKDF-Expand-Label`函数执行过程中生成的标签（即`HkdfLabel.label`），以及为生成输出而提供给`HKDF-Expand`函数的值的一部分如下：

> client in: 00200f746c73313320636c69656e7420696e00
> server in: 00200f746c7331332073657276657220696e00
> quicv2 key: 001010746c73313320717569637632206b657900
> quicv2 iv: 000c0f746c7331332071756963763220697600
> quicv2 hp: 00100f746c7331332071756963763220687000

初始密钥通常是：
```
initial_secret = HKDF-Extract(initial_salt, cid)
    = 2062e8b3cd8d52092614b8071d0aa1fb
      7c2e3ac193f78b280e72d8f5751f6aba
```

用于保护客户端数据包的密钥是：
```
client_initial_secret
    = HKDF-Expand-Label(initial_secret, "client in", "", 32)
    = 14ec9d6eb9fd7af83bf5a668bc17a7e2
      83766aade7ecd0891f70f9ff7f4bf47b

key = HKDF-Expand-Label(client_initial_secret, "quicv2 key", "", 16)
    = 8b1a0bc121284290a29e0971b5cd045d

iv  = HKDF-Expand-Label(client_initial_secret, "quicv2 iv", "", 12)
    = 91f73e2351d8fa91660e909f

hp  = HKDF-Expand-Label(client_initial_secret, "quicv2 hp", "", 16)
    = 45b95e15235d6f45a6b19cbcb0294ba9
```

用于保护服务端数据包的密钥是：
```
server_initial_secret
    = HKDF-Expand-Label(initial_secret, "server in", "", 32)
    = 0263db1782731bf4588e7e4d93b74639
      07cb8cd8200b5da55a8bd488eafc37c1

key = HKDF-Expand-Label(server_initial_secret, "quicv2 key", "", 16)
    = 82db637861d55e1d011f19ea71d5d2a7

iv  = HKDF-Expand-Label(server_initial_secret, "quicv2 iv", "", 12)
    = dd13c276499c0249d3310652

hp  = HKDF-Expand-Label(server_initial_secret, "quicv2 hp", "", 16)
    = edf6d05c83121201b436e16877593c3a
```
