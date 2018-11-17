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

### 备注


![BMcomment](https://github.com/DangDang-Chain/DebugList/blob/master/Screen%20Shot%202018-11-16%20at%208.37.05%20PM.png)

以上为BM对问题的解答，使用checkpoint进行硬分叉。 但是以上仅仅是因为undo history的上限已经积累足够多造成的，如果无法确保有足够的服务器/witness在正常运行，以上问题仍然会在很短的时间内复现；如果服务器本地没有进行备份或者其他节点没有备份区块头信息，也无法使用checkpoint进行分叉。因为没有有效存储区块头意味着无人对网络进行有效的维护。




