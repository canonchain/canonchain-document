# 合约的Logs解析

`Events` 和 `Logs` 属于一个概念，可以理解为：通过 Logs 实现 Events（事件） 功能，智能合约代码通过 Logs 将日志写入区块链中。

## 步骤

- 第一步：通过 RPC接口 [status](https://canonchain.readthedocs.io/zh/latest/source/JSON-RPC-%E6%8E%A5%E5%8F%A3.html#status) 获取链上的最新状态
    - 返回结果中 `last_stable_block_index`，是链上的最新状态的数据。
    - 需要提供一个值（假设为变量`dbStableIndex`）作为链上数据的第一次查询起点
        - 推荐用合约部署成功所在块的 `stable_index` 作为查询起点。
- 第二步：比较 `dbStableIndex` 和 `last_stable_block_index` 的值
    - `dbStableIndex` 小于 `last_stable_block_index`
        - 进入下一步。
    - `dbStableIndex` 不小于 `last_stable_block_index`
        - 表示已经读取到链上的最新数据，请间隔N秒后再次从第一步开始获取。
- 第三步：通过RPC接口 [logs](https://canonchain.readthedocs.io/zh/latest/source/JSON-RPC-%E6%8E%A5%E5%8F%A3.html#logs) 来获取日志数据。
    - 将 `dbStableIndex` 加一，作为参数 `from_stable_block_index` 。
    - 将 `last_stable_block_index` 作为参数 `to_stable_block_index` 。
    - 调用时可以通过参数 account 和 topics 进行数据过滤
        - account 可以在合约部署成功的后，通过返回的交易哈希查询 [block-state](https://canonchain.readthedocs.io/zh/latest/source/JSON-RPC-%E6%8E%A5%E5%8F%A3.html#block-state) 得到。
- 第四步：遍历 `logs` 数组
    - 根据需求解析和储存需要的数据。
    - logs内的数据说明
        - `item.account`：合约的触发账号。
        - `item.topics`
            - `topics[0]`是 `sha3(event名字(参数1类型,参数2类型))` 的值。
                - 如果是匿名事件，则不存在这个值。
            - 如果合约事件中的参数被标记为`indexed`, 他们的值会按照顺序出现在 `topics` 中。
        - `item.data`：如果合约事件中的参数未被标记为`indexed`，他们的值会按照顺序出现在 `data` 字段中。
- 第五步：循环结束后
    - 用第三步请求参数中 `to_stable_block_index` ，更新 `dbStableIndex` 的值。
    - 进入第一步。