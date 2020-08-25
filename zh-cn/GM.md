## 国密算法

### SM2

1. 使用推荐曲线 SM2P256V1，椭圆曲线各个参数为 

```python
a = 'FFFFFFFEFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF00000000FFFFFFFFFFFFFFFC' # 系数 a
b = '28E9FA9E9D9F5E344D5A9E4BCF6509A7F39789F515AB8F92DDBCBD414D940E93' # 系数 b
p = 'FFFFFFFEFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF00000000FFFFFFFFFFFFFFFF' # 素数域Fp

Gx = '32C4AE2C1F1981195F9904466A39C9948FE30BBFF2660BE1715A4589334C74C7' # G 点的 x 坐标
Gy = 'BC3736A2F4F6779C59BDCEE36B692153D0A9877CC62A474002DF32E52139F0A0' # G 点的 y 坐标
n = 'FFFFFFFEFFFFFFFFFFFFFFFFFFFFFFFF7203DF6B21C6052B53BBF40939D54123' # G 点的阶
```

2. 公钥一律以压缩后的形式保存或发送，公钥压缩和解压缩以 《SM2椭圆曲线公钥密码算法 第1部分:总则》第四节作为标准

3. SM2 签名使用 ```userid@soie-chain.com``` 作为 userid，签名结果以 r 和 s 按顺序拼接的方式保存，总共64各字节。

4. SM2 公钥加密的结果以 C1C2C3 的形式保存，其中 C1 是以 0x04 开头的未经过压缩的公钥，C2 是真正加密后的密文，C3 是 SM3 摘要

### SM3

sm3 符合 《SM3密码杂凑算法》中的标准。

### SM4

sm4 符合《无线局域网产品使用的 SMS4 密码算法》中的标准。一律使用 ECB 的方式加解密，密钥长度 16 个字节。如果需要对消息进行填充，则按照如下步骤进行填充：

1. 以字节为单位计算消息的长度，因为消息的长度小于 ```2^32```，我们会得到一个 32 bit 的无符号整数 ```l```

2. 把 ```l``` 采用大端编码的方式，编码成 4 个字节长度的字节串 ```arr0```

3. 计算消息原文的长度加上4以后，模16的加法逆元 ```m```

```typescript
const m = 16 - ((msg.length + 4) % 16) // C-style 编程语言的模运算符号是 %
```

4. 构造一个长度为 ```m``` 的字节数组 ```arr1```，用 ```0x00``` 填充

5. 把 ```arr0```、```msg``` 和 ```arr1``` 拼接得到填充后的字节串 ```padded```，而且填充后的字节串的长度一定是 16 的倍数。


同理我们可以从 ```padded```字节串拿到 msg：

1. 读取前四个字节，并且根据大端编码得到 32 bit 无符号整数 ```l```，这个 ```l``` 就是消息原文的长度

2. 继续读取 ```l``` 个字节，得到消息原文 ```msg```
