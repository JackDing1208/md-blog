# HTTPS

### 产生原因

由于HTTP采用明文传输，存在安全隐患，一个安全的通讯协议应该保证以下几点：

- **通信内容的保密性**

- **通信双方身份的真实性**

- **通信内容的完整性**

后续便推出了HTTPS技术对传输的数据进行加密，目前已经十分普及。

### 加密方法

Https 怎样保证数据传输安全？再讲讲 Https的原理之前必须先聊一聊数据加密，目前有以下几种加密方式：

1. 对称加密 ： 加密和解密数据使用同一个密钥。这种加密方式的优点是速度很快，常见对称加密的算法有 AES；
2. 非对称加密： 加密和解密使用不同的密钥，叫公钥和私钥。数据用公钥加密后必须用私钥解密，数据用私钥加密后必须用公钥解密。一般来说私钥自己保留好，把公钥公开给别人，让别人拿自己的公钥加密数据后发给自己，这样只有自己才能解密。 这种加密方式的特点是速度慢，CPU 开销大，常见非对称加密算法有 RSA；
3. Hash： hash 是把任意长度数据经过处理变成一个长度固定唯一的字符串，但任何人拿到这个字符串无法反向解密成原始数据（解开你就是密码学专家了），Hash 常用来验证数据的完整性。常见 Hash 算法有 MD5（已经不安全了）、SHA1、SHA256

### 实现过程

- 如果AB双方直接采用AES对称加密，密钥如何约定？先明文传密钥会导致后面的加密过程白费

  双方首先通过非对称加密RSA约定密钥，然后再用AES密钥对数据进行对称加密，既A先公布自己的公钥，B将后续AES的密钥使用公钥进行加密传给A，A用自己的私钥进行解密得到了约定好的AES密钥，后续再基于此AES密钥进行加密传输

- 那么A要如何公布自己的公钥让B知道？

  A会首先去找C机构去申请一份证书，证书里包含B的公钥和其他相关信息，然后A会在B每次发起HTTPS请求时把证书发给B，B确认证书的真实性后便可以拿到公钥

- B要如何确定自己收到的公钥是真的？

  证书主要包含：C机构的名称，A的名称，经过C私钥加密过的A公钥，经过C私钥加密过的证书签名

  证书签名是根据证书内容通过Hash（SHA256）加密的一串文本

  B通过证书中C机构的名称能够查到（浏览器跟操作系统一般都支持）C的公钥，通过C的公钥解密得到A公钥和证书原始签名，然后B通过Hash（SHA256）将证书内容加密后与原始签名比较便可以确认证书的真实性

- 即使中间方无法获取数据内容，但可以随便删改，如果保证完整性？

  双方可以将传输内容进行Hash加密，将得到的结果明文传给对方，对方收到内容时也进行Hash加密，如果与能符合则收到内容是真实完整的

### SSL

以上流程便是HTTPS在HTTP基础上增加的SSL安全层，并在此基础上衍生出了TSL，基本原理是类似的

### 主要缺点

1. 申请SSL证书要钱，功能越强大的证书费用越高
2. HTTPS协议多次握手，导致页面的加载时间延长
3. SSL涉及到的安全算法会消耗 CPU 资源，对服务器资源消耗较大
4. HTTPS连接缓存不如HTTP高效，会增加数据开销和功耗





参考：

###### [一个故事让你彻底理解 Https](https://zhuanlan.zhihu.com/p/31880655)



