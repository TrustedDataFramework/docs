## 12.1 指令集
&#160;&#160;&#160;&#160;&#160;&#160;Wasm二进制文件中的代码也由一条一条的指令构成。同样，Wasm指令也包含两	部分信息：操作码（Opcode）和操作数 （Operands）。

&#160;&#160;&#160;&#160;&#160;&#160;Wasm操作码固定为一个字节，因此最多能表示256条指令，这一点和Java字节码一样。

&#160;&#160;&#160;&#160;&#160;&#160;Wasm1.0规范一共定义了172条指令，这些指令按功能可以分为5大类，分别是：

&#160;&#160;&#160;&#160;&#160;&#160;控制指令（Control Instructions），共13条。

&#160;&#160;&#160;&#160;&#160;&#160;参数指令（Parametric Instructions），共2条。

&#160;&#160;&#160;&#160;&#160;&#160;变量指令（Variable Instructions），共5条。

&#160;&#160;&#160;&#160;&#160;&#160;内存指令（Memory Instructions），共25条。

&#160;&#160;&#160;&#160;&#160;&#160;数值指令（Numeric Instructions），共127条。
## 12.2 执行结构
&#160;&#160;&#160;&#160;&#160;&#160;WebAssembly文件(称之为模块)总体上由三块组成：魔数(固定值:0x6d736100，小端存储)、版本号(当前值:0x00000001，小端存储)、以及若干个区(section)。

&#160;&#160;&#160;&#160;&#160;&#160;其中，每个区由三部分组成:类型、长度以及实际数据。 

&#160;&#160;&#160;&#160;&#160;&#160;WebAssembly二进制格式中使用LEB128编码表示整数和字符串长度信息，因为WebAssembly是在网络上传输的，所以该格式为了尽量缩小文件体积，在内部广泛使用了数据压缩格式leb128,leb128是变长的整数压缩编码形式。

&#160;&#160;&#160;&#160;&#160;&#160;因为在很多情况下，比如一个32位的整数在大部分时间存储的值只需要一个8位的字节存储即可，但是将来又有可能需要32位，因此可以采用采用leb128编码。

&#160;&#160;&#160;&#160;&#160;&#160;leb128采用的方式是从低字节开始，每个字节中的最高位不是存储实际的值，而是用来作为标志位，当该位置位时，表示下一字节还有数据，否则表示下一字节没有数据，没有数据的字节直接省略，从而达到了数据压缩的目的。
   	
## 12.3 临时存储
&#160;&#160;&#160;&#160;&#160;&#160;线性内存 是一段 按字节寻址的连续存储区间， 范围从0 到一个可变 内存容量 。 这个容量通常是WebAssembly页容量的倍数, WebAssembly的页容量被固定为64KiB（尽量未来可能添加可选的更大页容量支持）。可以用 grow_memory运算符动态增加线性内存容量。

&#160;&#160;&#160;&#160;&#160;&#160;线性内存可以被认为是一个无类型的字节数组，嵌入器是如何把这个数组映射到进程自己的 虚拟内存 中并没给出明确说明。线性内存是沙盒隔离的，它不依赖其它的线性内存、 执行引擎的内部数据结构执行堆栈、局部变量、其它进程的内存。

&#160;&#160;&#160;&#160;&#160;&#160;局部变量

&#160;&#160;&#160;&#160;&#160;&#160;每个函数都有一些固定的，预声明的局部变量，它们占用函数内部的单个索引空间。 

&#160;&#160;&#160;&#160;&#160;&#160;参数被当作局部变量处理。 局部变量没有地址和线性内存别名。 局部变量具有值类型，函数开头将局部变量的类型初始化为相应的零值（整型值初始为0，浮点数初始为+0），形参则被初始化为传递给函数的实参值。

&#160;&#160;&#160;&#160;&#160;&#160;- get_local: 获取局部变量当前值

&#160;&#160;&#160;&#160;&#160;&#160;- set_local: 设置局部变量当前值

&#160;&#160;&#160;&#160;&#160;&#160;- tee_local: 类似 set_local, 设置局部变量当前值后返回被设置的新值

&#160;&#160;&#160;&#160;&#160;&#160;关于局部变量索引空间和类型的细节将进一步明确， 例如， 类型为i32和i64的局部变量必须是相邻的，还是被其它变量分开的等等。

&#160;&#160;&#160;&#160;&#160;&#160;全局变量

&#160;&#160;&#160;&#160;&#160;&#160;全局变量存储固定值类型的单个值，并且可以声明为可变的或不可变的。这为WebAssembly提供了与任何线性存内存都不相交的内存位置，因此不能任意地作为位来别名。

&#160;&#160;&#160;&#160;&#160;&#160;全局变量只能从模块内定义的 全局索引空间中通过整数索引的方式获取。全局变量要么是被导入 ， 要么是模块内定义的。这两种方式对后续的全局变量访问没有区别。

&#160;&#160;&#160;&#160;&#160;&#160;- get_global: 获取全局变量的当前值

&#160;&#160;&#160;&#160;&#160;&#160;- set_global: 设置全局变量的当前值

&#160;&#160;&#160;&#160;&#160;&#160;- set_global
设置不可变全局变量索引会导致验证异常

## 12.4 编译器前端
&#160;&#160;&#160;&#160;&#160;&#160;把前端代码转换成.wasm文件，再把文件放入部署合约事务的payload中，广播到节点。
## 12.5 支持语言
&#160;&#160;&#160;&#160;&#160;&#160;typescript, rust, c, c++, javascript, golang

## 12.6 智能合约示例
<b>注：详细的智能合约部署和调用说明，具体参见 《[智能合约详细说明](../zh-cn/Contracts.md)》。</b>

### 12.6.1 入门
以下是一个智能合约 hello world 示例：
```typescript
import {DB, Result, log, RLP, Context} from "../lib";

const KEY = Uint8Array.wrap(String.UTF8.encode('key'));

// every contract should had a function named by init
// which will be called at most once when contract deployed
export function init(): void{
    log("contract deployed successfully by index.ts")
}

export function increment(): void {
    let i = DB.has(KEY) ?  RLP.decodeU64(DB.get(KEY)) : 0;
    i++;
    log("call contract successful counter = " + i.toString());
    DB.set(KEY, RLP.encodeU64(i));
}

export function get(): void{
    let i = DB.has(KEY) ?  RLP.decodeU64(DB.get(KEY)) : 0;
    Result.write(RLP.encodeU64(i))
}

export function getN(): void{
    let i = DB.has(KEY) ?  RLP.decodeU64(DB.get(KEY)) : 0;
    const args = Context.args();
    assert(args.method === 'getN', 'method is getN');
    const j = RLP.decodeU64(args.parameters);
    Result.write(RLP.encodeU64(i + j))
}

export function addN(): void {
    const args = Context.args();
    let i = DB.has(KEY) ?  RLP.decodeU64(DB.get(KEY)) : 0;
    i+= RLP.decodeU64(args);
    DB.set(KEY, RLP.encodeU64(i));
}
```   
&#160;&#160;&#160;&#160;&#160;&#160;在这个智能合约中，第一个方法是 init 方法，这个方法只有在合约部署时会被调用。

&#160;&#160;&#160;&#160;&#160;&#160;在智能合约的第一行引入了 DB 这个依赖，在智能合约中可以通过 DB 操作合约存储，例如 increament 方法在每次触发时会把 DB 中读取一个整数，再把整数加一，然后再保存到 DB 中。

&#160;&#160;&#160;&#160;&#160;&#160;该合约部署成功后，如果想调用 increment 方法，需要构造事务，构造事务的伪代码如下:
```js
// 构造 payload 需要把方法长度作为第一个字节拼在方法名的 ascii 编码之前
const method = Buffer.from('increment', 'ascii')
const prefix = Buffer.of([method.length])
const tx = {
    "version": 1634693120,
    "type": 3,
    "createdAt": "2020-07-29T07:16:40Z",
    "nonce": 1,
    "from": "你的公钥",
    "gasPrice": 0,
    "amount": 0,
    "payload": Buffer.concat([prefix, method]).toString('hex'), 
    "to": "合约的地址",
    "signature": "****",
    "hash": "**",
}
```
&#160;&#160;&#160;&#160;&#160;&#160;如果想查看这个 i 的最新数值，可以调用如下的伪代码

```js
const rlp = require('rlp') // https://www.npmjs.com/package/rlp
const BigInteger = require('bigi') // https://www.npmjs.com/package/bigi

// 构造 parameters 同样需要把方法长度作为第一个字节拼在方法名的 ascii 编码之前
const contractAddress = '****'
const method = Buffer.from('get', 'ascii')
const prefix = Buffer.of([method.length])
const parameters = Buffer.concat([prefix, method]).toString('hex')
axios.get(`localhost:8888/rpc/contract/${contractAddress}?parameters=${parameters}`)
  .then(r => {
    const d = r.data.data
    // 因为 合约中 Result.write 的是 i 的 rlp 编码，所以需要再解码一次
    const i = BigIneger.fromBuffer(rlp.decode(Buffer.from(d, 'hex')))
    console.log(`i = ${i.intValue()}`)
  })
```
### 12.6.2  方法调用
&#160;&#160;&#160;&#160;&#160;&#160;在外界与合约交互有两种方式：

1.发起请求

&#160;&#160;&#160;&#160;&#160;&#160;若想在查看合约的同时加入参数，可以用二进制的方式传入，例如要调用以上合约的 getN 方法，并且把 j 作为参数传递：
```js
const contractAddress = '****' // 合约的地址
const method = Buffer.from('getN', 'ascii')
const prefix = Buffer.of([method.length])
const j = rlp.encode(123456) // 使用 rlp 专成 Uint8 Array
const parameters = Buffer.concat([prefix, method, j]).toString('hex')
axios.get(`localhost:8888/rpc/contract/${contractAddress}?parameters=${parameters}`)
  .then(r => {
    const d = r.data.data
    // 因为 合约中 Result.write 的是 i 的 rlp 编码，所以需要再解码一次
    const i = BigIneger.fromBuffer(rlp.decode(Buffer.from(d, 'hex')))
    console.log(`i = ${i.intValue()}`)
  })
```
&#160;&#160;&#160;&#160;&#160;&#160;通过发起请求智能查看合约的状态，无法改变合约的存储，如果在查看合约状态时试图改写 DB，接口会报错

2.构造事务

&#160;&#160;&#160;&#160;&#160;&#160;只有通过构造事务采可以改变合约的存储状态，例如方法 addN()，调用该方法的事务如下：
```js
const rlp = require('rlp') // https://www.npmjs.com/package/rlp
const method = Buffer.from('addN', 'ascii')
const prefix = Buffer.of([method.length])
const args = rlp.encode(123456)

const tx = {
    "version": 1634693120,
    "type": 3,
    "createdAt": "2020-07-29T07:16:40Z",
    "nonce": 1,
    "from": "你的公钥",
    "gasPrice": 0,
    "amount": 0,
    "payload": Buffer.concat([prefix, method, args]).toString('hex'), 
    "to": "合约的地址",
    "signature": "****",
    "hash": "**",
}
```
&#160;&#160;&#160;&#160;&#160;&#160;如果通过构造事务调用合约，可以通过在payload后面拼接上参数，其他和区块链有关的参数也可以通过 Context 类获得
```ts
const header = context.header(); // 获得区块头
const tx = context.transaction(); // 获取当前的事务
const contract = context.contract(); // 获取合约自身
```