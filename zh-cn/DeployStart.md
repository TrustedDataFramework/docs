## 4.1 参数说明
```
sunflower:
    assert: 'false' # 是否开启断言，默认是 false
    validate: 'false' # 启动时是否校验本地数据，如果设置为true，启动时会校验账本数据
    libs: 'local/jar' # jar包路径，用于加载外部的共识插件
    secret-store: "" # 证书的路径，若填写，节点启动后会打印出一个公钥并且进入阻塞，用户通过工具生成证书文件保存到这个路径后，节点会成功加载证书
```
## 4.2 启动步骤
1.安装jdk，版本要求在8以上 
http://openjdk.java.net/install/

2.下载好打包好的 jar 文件，名称为
sunflower-core-0.0.1-SNAPSHOT.jar

3.下载样板配置文件，根据自己的需求修改配置
https://yongyang-common.oss-cn-beijing.aliyuncs.com/local-0.yml

4.在命令行输入
```
 Java -jar sunflower-core-0.0.1-SNAPSHOT.jar --spring.config.location=local-0.yml
```
 
## 4.3 启动说明

&#160;&#160;&#160;&#160;&#160;&#160;TDS 采用 yml 文件作为参数配置文件，可以在启动时用环境变量SPRING_CONFIG_LOCATION 指定好自定义的配置文件。 例如:
```
java -jar sunflower*.jar --spring.config.location=classpath:application.yml,$HOME/Documents/local.yml
```

&#160;&#160;&#160;&#160;&#160;&#160;文件路径之间以逗号分割，后面的配置会覆盖前面的配置。 除了环境变量配置，也可以用命令行参数指定配置文件，例如
```
java -jar sunflower*.jar --spring.config.location=classpath:application.yml
```

&#160;&#160;&#160;&#160;&#160;&#160;配置文件中的参数都可以用相应的命令函参数覆盖， 例如配置文件中的配置项 spring.datasource.url 可以在启动时用命令行参数覆盖。
```
java -jar app.jar --spring.datasource.url="jdbc:h2:mem:test"
```

##  4.4 证书
##  4.5 编码格式
&#160;&#160;&#160;&#160;&#160;&#160;递归前缀编码(RLP)：https://github.com/ethereum/wiki/wiki/RLP 一种二进制序列化规范，优点是紧凑，缺点是最大只支持对4G以下的内容进行编解码。

&#160;&#160;&#160;&#160;&#160;&#160;java 可以采用注解的方式进行 rlp 编码和解码：https://github.com/TrustedDataFramework/java-rlp

&#160;&#160;&#160;&#160;&#160;&#160;javascript 或 nodejs 中使用 rlp 编码可参考 https://github.com/ethereumjs/rlp