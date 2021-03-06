---
title: 账号管理
weight: 20
---

Starcoin 节点内置了一个去中心化的钱包，用户可以通过账号相关的接口以及命令来管理自己的账号。

节点启动的时候，会自动创建一个默认账号，默认密码是空。默认可以通过账号相关的命令进行变更。以下命令需要连接到控制台进行操作，连接方式请参看[使用 starcoin 控制台](./console)。



 1. 通过 account create 命令可以创建账号

```bash
starcoin% account create -p my-pass
+------------+--------------------------------------------------------------------+
| address    | 0x8d885d806c14654832aa371c3c980153                                 |
+------------+--------------------------------------------------------------------+
| is_default | false                                                              |
+------------+--------------------------------------------------------------------+
| public_key | 0xf0a2cee9d7c85a40f3f217782b449fab9ba73fa11ab210f11d12305fdf57b908 |
+------------+--------------------------------------------------------------------+

```

2. 通过 account show 命令可以查看账号状态

```bash
starcoin% account show 0x8d885d806c14654832aa371c3c980153
+--------------------+--------------------------------------------------------------------+
| account.address    | 0x8d885d806c14654832aa371c3c980153                                 |
+--------------------+--------------------------------------------------------------------+
| account.is_default | false                                                              |
+--------------------+--------------------------------------------------------------------+
| account.public_key | 0xf0a2cee9d7c85a40f3f217782b449fab9ba73fa11ab210f11d12305fdf57b908 |
+--------------------+--------------------------------------------------------------------+
| auth_key           | 0xbc0b37f099741399c30dcd09cfd8a6118d885d806c14654832aa371c3c980153 |
+--------------------+--------------------------------------------------------------------+
| sequence_number    |                                                                    |
+--------------------+--------------------------------------------------------------------+
```

- address 是账户地址。
- public_key 是账户地址对应的公钥。
- auth_key 是认证秘钥，最后是需要写到链上去的。 

> 注意，创建账户只是在 starcoin node里创建一对密钥，并不会更新链的状态。所以 balance 和  sequence_number 此时还是空的。以上信息都属于公开信息，只有私钥是需要用户保密的。


3. 通过 account list 可以查看账号列表

```bash
starcoin% account list
+------------------------------------+------------+--------------------------------------------------------------------------------------------------------------------------------------+
| address                            | is_default | public_key                                                                                                                           |
+------------------------------------+------------+--------------------------------------------------------------------------------------------------------------------------------------+
| 0xddf5d370b6aae8251dacc99d1ff6fe94 | true       | 0xaaf0b46c8a6bb88322e047aebdc90b0be7415583230d2dccff7b3fbe1fcfbfec                                                                   |
+------------------------------------+------------+--------------------------------------------------------------------------------------------------------------------------------------+
| address                            | is_default | public_key                                                                                                                           |
+------------------------------------+------------+--------------------------------------------------------------------------------------------------------------------------------------+
| 0x8d885d806c14654832aa371c3c980153 | false      | 0xf0a2cee9d7c85a40f3f217782b449fab9ba73fa11ab210f11d12305fdf57b908                                                                   |
+------------------------------------+------------+--------------------------------------------------------------------------------------------------------------------------------------+
```

- is_default: 表示是否为默认账号。很多命令如果需要账号参数，但用户没有传递，则会使用默认账号。如果节点开启了挖矿客户端，也会使用默认账号进行挖矿。

4. 通过 account default 命令查看或者变更默认账号

查看默认账号地址：

```bash
account default
```
将 0x8d885d806c14654832aa371c3c980153 设置位默认地址。
```bash
account default 0x8d885d806c14654832aa371c3c980153
```

> 注意：改变默认账号后，有的服务不会自动使用新的默认账号，最好重启一下节点。

5. 通过 account export/import 命令导出导入账号

为了避免磁盘损坏等原因导致自己的资产损失，备份自己的私钥非常重要。

执行以下命令: 
```bash
account export 0x8d885d806c14654832aa371c3c980153 -p my-pass
```
即可导出 0x8d885d806c14654832aa371c3c980153 的私钥。

执行以下命令:

```bash
account import -i <private-key> -p my-pass 0x8d885d806c14654832aa371c3c980153
```

即可导入 0x8d885d806c14654832aa371c3c980153 账号。这个命令也可以用于将账号导入到不同的节点上，用来做节点迁移。
