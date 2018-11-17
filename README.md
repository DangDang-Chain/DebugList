# DebugList






## `Undo` history



![BugInfo1](https://github.com/DangDang-Chain/DebugList/blob/master/ddddd.jpg)


错误信息 __`The database does not have enough undo history to support a blockchain with so many missed blocks. Please add a checkpoint if you would like to continue applying blocks beyond this point.
`__

### 原因

因为服务器硬件限制和witness节点数目限制，积累了足够多的missing block，以致造成系统崩溃；

### 处理方法

使用 __`checkpoint`__ 进行硬分叉。

在原有启动witness的命令中添加

```c
--checkpoint '[40902,"00009fc6d4e24db66e13af461b94063165999bfa"]' --enable-stale-production 
// 替换区块编号和对应的哈希值
```

在log历史不被覆盖的情况下，文件的log信息/cli中可以检索

```json
new >>> info
info
{
  "head_block_num": 40902,
  "head_block_id": "00009fc6d4e24db66e13af461b94063165999bfa",
  "head_block_age": "4 hours old",
  "next_maintenance_time": "4 hours ago",
  "chain_id": "5508f5f743717fe2c78445364f62a72badd7532974d26f089af2062228b532eb",
...
}
```



