## 6.1 事务结构


| 字段名     |   类型   | 说明 |
| ---- | ---- | ---- |
| version | int | 事务版本号 PoA=1634693120,PoW=7368567,PoS=7368563 |
| type    |   int   | 0=COINBASE,1=转账,2=合约部署,3=合约调用|
|  createdAt  |   long   | 事务的构造时间，用 unix epoch 秒数表示 |
| nonce | long | 事务的序号，coinbase事务的 nonce 等于区块高度 |
| from| bytes | 事务发送者的公钥 |
| gasPrice | long | 事务的手续费价格 |
| amount | long | 转账、后者在合约调用时的转账金额|
| payload | bytes | 载荷 |
| to | bytes |  转账的接收者或者被调用的合约|
| signature | bytes | 签名 |
| hash | bytes | 事务哈希 |


## 6.2 amount 的不同含义

1. 对于 coinbase 事务，amount 是经济奖励的数量
2. 对于转账事务，amount 是转账的数量
3. 对于合约部署的事务，amount 必须为 0 
4. 对于合约调用的事务，amount 的金额会被转到合约的创建者的账户下

## 6.3 payload 的不同含义

1. coinbase 事务和 转账事务的 payload 一般为空，特别的是 PoA 共识的 payload 填写的是出块者的公钥
2. 对于合约部署事务，payload 是智能合约 wasm 字节码
3. 对于合约调用事务，payload 是调用智能合约的二进制参数，构造方法是把智能合约方法名长度放在第一个字节，后面跟方法名的 acii 编码，剩余的就是针对具体调用的方法的参数