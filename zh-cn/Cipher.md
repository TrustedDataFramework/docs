# 十、密码算法
&#160;&#160;&#160;&#160;&#160;&#160;密码算法采用国密算法,由国家密码管理局于2010年12月17日发布，主要实现为sm2、sm3和sm4
## 10.1 简介
### SM2 

&#160;&#160;&#160;&#160;&#160;&#160;SM2 椭圆曲线公钥密码算法是我国自主设计的公钥密码算法，包括SM2-1椭圆曲线数字签名算法，SM2-2椭圆曲线密钥交换协议，SM2-3椭圆曲线公钥加密算法，分别用于实现数字签名密钥协商和数据加密等功能。SM2算法与RSA算法不同的是，SM2算法是基于椭圆曲线上点群离散对数难题，相对于RSA算法，256位的SM2密码强度已经比2048位的RSA密码强度要高。

&#160;&#160;&#160;&#160;&#160;&#160;椭圆曲线参数并没有给出推荐的曲线，曲线参数的产生需要利用一定的算法产生。但在实际使用中，国密局推荐使用素数域256 位椭圆曲线，其曲线方程为y^2= x^3+ax+b（其中p是大于3的一个大素数，n是基点G的阶，Gx、Gy 分别是基点G的x与y值，a、b是随圆曲线方程y^2= x^3+ax+b的系数）。

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

&#160;&#160;&#160;&#160;&#160;&#160;SM3 杂凑算法是我国自主设计的密码杂凑算法，适用于商用密码应用中的数字签名和验证消息认证码的生成与验证以及随机数的生成，可满足多种密码应用的安全需求。为了保证杂凑算法的安全性，其产生的杂凑值的长度不应太短，例如MD5输出128比特杂凑值，输出长度太短，影响其安全性SHA-1算法的输出长度为160比特，SM3算法的输出长度为256比特，因此SM3算法的安全性要高于MD5算法和SHA-1算法。

### SM4

&#160;&#160;&#160;&#160;&#160;&#160;SM4 分组密码算法是我国自主设计的分组对称密码算法，用于实现数据的加密/解密运算，以保证数据和信息的机密性。要保证一个对称密码算法的安全性的基本条件是其具备足够的密钥长度，SM4算法与AES算法具有相同的密钥长度分组长度128比特，因此在安全性上高于3DES算法。

&#160;&#160;&#160;&#160;&#160;&#160;SM4 符合《无线局域网产品使用的 SMS4 密码算法》中的标准。一律使用 ECB 的方式加解密，密钥长度 16 个字节。如果需要对消息进行填充，则按照如下步骤进行填充：

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

## 10.2参数配置
```yml
sunflower:
  crypto:
    hash: 'sm3' #哈希计算
    ec: 'sm2' #非对称加密
    ae: 'sm4' #对称加密
```
## 10.3 Keystore
keystore 用于保存用户的私钥
```json
{
  "publicKey" : "02ef5b1a65b7f2afbc20ecd0f1400892ea8c4e2c86fd0491abcb8be8af7f1f6a41", // 用户的公钥

  "crypto" : {
    "cipher" : "sm4-128-ctr", // 使用的对称加密算法 
    "cipherText" : "f078aefe661bc4498d686216e263c77a9026dcb4249d935c0b26b0b289cab098", // 加密过后的私钥

    "iv" : "ce69a3f220a7d6e6eea04eb927e9f4d1", 
    "salt" : "cfa496f673a4eeb508d301822b35b867aa05533225774fd47509908e6357e0cd"
  },
  "id" : "39453f15-b72d-4599-a86e-6d7459fa19d7",
  "version" : "1",
  "mac" : "345a86d380a043d20f36712ebb4bed37bdab412e73a290cab5aee6203c2ef83a",
  "kdf" : "sm2-kdf",
  "address" : "c86d486ac528ff14c17b9a9190b4d3c79a0291a8"
}
 ```
keystore 的生成过程用伪代码表示:
```
keystore = {}
sk = b'********' # 私钥password = '********' # 用户输入的密码salt =
randbytes(32) # 生成随机盐iv = randbytes(16) # 生成随机向量key = sm3(salt
+ password.encode('ascii'))[:16] # 推导出keykeystore['salt'] =
salt.hex()keystore['iv'] = iv.hex()keystore['ciphertext'] =
sm4.encrypt_ctr_nopadding(key, iv, sk) # 对私钥进行加密保存keystore['mac']
= sm3(key + ciphertext).hex() # 生成 mackeystore['id'] == uuid()
keystore['version'] = '1'
```
keystore 的读取过程用伪代码表示：
```
password = '********' # 用户输入的密码salt =
bytes.fromhex(keystore['salt']) # 盐iv = bytes.fromhex(keystore['iv']) #
ivkey = sm3(salt + password.encode('ascii'))[:16]cipher =
bytes.fromhex(keystore['ciphertext'])sk = sm4.decrypt_ctr_nopadding(key,
iv, cipher) # 读取到私钥
```
<b>注：具体国密和keystore调用可以参考SDK使用</b>