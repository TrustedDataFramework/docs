# 十、密码算法
&#160;&#160;&#160;&#160;&#160;&#160;密码算法采用国密算法,由国家密码管理局于2010年12月17日发布，主要实现为sm2、sm3和sm4
## 10.1 简介
### SM2 

&#160;&#160;&#160;&#160;&#160;&#160;SM2椭圆曲线公钥密码算法是我国自主设计的公钥密码算法，包括SM2-1椭圆曲线数字签名算法，SM2-2椭圆曲线密钥交换协议，SM2-3椭圆曲线公钥加密算法，分别用于实现数字签名密钥协商和数据加密等功能。SM2算法与RSA算法不同的是，SM2算法是基于椭圆曲线上点群离散对数难题，相对于RSA算法，256位的SM2密码强度已经比2048位的RSA密码强度要高。

&#160;&#160;&#160;&#160;&#160;&#160;椭圆曲线参数并没有给出推荐的曲线，曲线参数的产生需要利用一定的算法产生。但在实际使用中，国密局推荐使用素数域256 位椭圆曲线，其曲线方程为y^2= x^3+ax+b（其中p是大于3的一个大素数，n是基点G的阶，Gx、Gy 分别是基点G的x与y值，a、b是随圆曲线方程y^2= x^3+ax+b的系数）。

### SM3

&#160;&#160;&#160;&#160;&#160;&#160;SM3杂凑算法是我国自主设计的密码杂凑算法，适用于商用密码应用中的数字签名和验证消息认证码的生成与验证以及随机数的生成，可满足多种密码应用的安全需求。为了保证杂凑算法的安全性，其产生的杂凑值的长度不应太短，例如MD5输出128比特杂凑值，输出长度太短，影响其安全性SHA-1算法的输出长度为160比特，SM3算法的输出长度为256比特，因此SM3算法的安全性要高于MD5算法和SHA-1算法。

### SM4

&#160;&#160;&#160;&#160;&#160;&#160;SM4分组密码算法是我国自主设计的分组对称密码算法，用于实现数据的加密/解密运算，以保证数据和信息的机密性。要保证一个对称密码算法的安全性的基本条件是其具备足够的密钥长度，SM4算法与AES算法具有相同的密钥长度分组长度128比特，因此在安全性上高于3DES算法。

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