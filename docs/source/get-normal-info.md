# 交易转账解析

本文档，用来描述如何使用RPC接口获取并解析交易，可以使用您熟悉的语言，按照下面流程进行获取。

## 必读信息
--- 

标准链采用 `DAG`结构 来组织链上的交易，一笔交易在DAG中是以一个`block`进行呈现；很多个`block`按照特定的方式进行连接，就组成了DAG结构。

**标准链没有确认数的概念，交易稳定(stable)即表示交易被确认，且不可逆**；已经稳定的交易我们会标记一个 **稳定交易索引**(stable block index)，表示每笔交易稳定后的全局顺序。

一笔完整的交易信息包含两部分，**交易(block)** 和 **交易状态(block_state)**；只有两部分都拿到,才算获取完整；

## 节点启动

通过RPC接口获取链上信息之前，需要在本地启动一个标准链节点，可以在 [标准链节点下载页面](http://dev.canonchain.com/download.html)中选择适合适文件进行下载。

**启动的命令如下**

```
# Windows
your_path\canonchain.exe --daemon --rpc --rpc_control --data_path=your_path\canonchain-data

# Mac
your_path/canonchain --daemon --rpc --rpc_control --data_path=/Users/your_name/your_path/canonchain-data

# Linux
your_path/canonchain --daemon --rpc --rpc_control --data_path=/Users/your_name/your_path/canonchain-data
```

**命令行参数说明**

- `--daemon`：开启节点并保持数据同步 
- `--rpc`：开启 **HTTP-RPC** 的只读权限
- `--rpc_control`：开启 **HTTP-RPC** 非只读权限
- `--data_path`：节点数据的存放目录

更多参数，请参考 [命令行参数文档](https://canonchain.readthedocs.io/zh/latest/source/Canonchain-%E5%91%BD%E4%BB%A4%E8%A1%8C%E5%8F%82%E6%95%B0.html)

## 交易获取和解析说明
---

- **第一步**：通过 RPC接口 [stable_blocks](https://canonchain.readthedocs.io/zh/latest/source/JSON-RPC-%E6%8E%A5%E5%8F%A3.html#stable-blocks) 批量获取已稳定的**交易(block)**。
- **第二步**：遍历第一步结果中的 `blocks`数组，判断交易的`type`值是否等于`2`。
    - 如果等于2
        - `from` 和 `content.to` 表示交易的源账户和目标账号，可以通过账号来过滤需要的交易。
        - `content.amount` 表示交易金额 (单位：10<sup>-18</sup>CZR)。
    - 如果不等于2，继续处理下一笔交易。
- **第三步**：用第二步拿到的Hash，通过RPC接口 [block_states](https://canonchain.readthedocs.io/zh/latest/source/JSON-RPC-%E6%8E%A5%E5%8F%A3.html#block-states) 获取 **交易状态(block_state)**
    1. 判断返回结果中的 `is_stable` 属性值是否等于`1`（交易稳定的冗余检查，如果不等于1，终止流程，请向我们上报BUG，非常感谢）。
    2. 判断返回结果中的 `stable_content.status` 属性值是否等于`0`
        - 如果等于0，表示交易成功，根据需求，解析记录需要的交易。
            - 使用变量 `localLastStableIndex` 记录 `stable_content.stable_index`的值。
        - 如果不等于0，表示交易失败，继续处理下一笔交易。
- **第四步**：遍历结束后判断第一步返回结果中的`next_index`的值。
    - 如果不为`null`，则用该值作为参数，从第一步开始继续获取数据
    - 如果为`null`，表示已经没有未获取的稳定交易了，请间隔N秒后再次从第一步开始获取（使用 `localLastStableIndex` 加1 作为参数 ）。

## 智能合约的内部交易解析
---

智能合约的内部交易转账可以通过 [block_traces](https://canonchain.readthedocs.io/zh/latest/source/JSON-RPC-%E6%8E%A5%E5%8F%A3.html#block-traces) 来获取，具体解析说明，请参照接口说明。