# 命令行参数

```
    $ canonchain --help
    NAME:
       canonchain - the canonchain command line interface

    USAGE:
       canonchain command [command options] [arguments...]
       
    VERSION:
       1.0-stable

    COMMANDS:
      --account_create             生成账户
      --account_remove             移除账户
        arguments：
          --account                  账户
      --account_import             导入账户
        arguments：
          --file                     账户文件
      --account_list               列出节点所有的账户
      --daemon                     开启节点 
      --help                       显示命令信息
      --version                    显示版本信息

    NODE OPTIONS:
      --network                    网络（默认：1 表示主网地址）
      --data_path                  节点数据目录
      --io_threads                 IO线程数       
      --bg_threads                 后台线程数
      --sync_threads               同步线程数

    RPC OPTIONS:
      --rpc                        开启HTTP-RPC服务
      --rpc_addr                   HTTP-RPC服务监听地址 (默认: 127.0.0.1)
      --rpc_port                   HTTP-RPC服务监听端口 (默认: 8765)
      --rpc_control                开启HTTP-RPC写入权限

    WS OPTIONS:
      --ws                         开启WebSocket服务  
      --ws_addr                    WebSocket服务监听地址 (默认: 127.0.0.1)
      --ws_port                    WebSocket服务监听端口 (默认: 8764)
      --ws_control                 开启WebSocket写入权限

    LOG OPTIONS:
      --console                    日志输出到控制台
      --max_size                   日志最大容量  
      --rotation_size              日志文件超过此设置建立新文件 
      --flush                      写入每条日志时刷新控制台日志和日志文件    
      --verbosity                  日志级别: none,error,warning,info,debug,trace (默认: info)
      --vmodule                    模块日志级别:  p2p=info,node=debug 逗号分隔符 (所有模块列表:node,p2p,rpc,db,sync)  
           
    P2P OPTIONS:
      --host                       P2P监听地址 (默认: 127.0.0.1)
      --port                       P2P监听端口 (默认: 30606) 
      --max_peers                  最大Peer数 (默认: 25)  
      --bootstrap_nodes            引导节点 
      --exemption_nodes            豁免惩罚节点 
      --nat                        开启NAT穿透

    WITNESS OPTIONS:               
      --witness                    开启见证人模式       
      --witness_account            见证人账户或者账户文件//账户:czr_3MnXfV9hbmxVPdgfrPqgUiH6N7VbkSEhn5VqBCzBcxzTzkEUxU 或账户文件:F:/czr_latest/test/czr_3MnXfV9hbmxVPdgfrPqgUiH6N7VbkSEhn5VqBCzBcxzTzkEUxU.json
      --password                   见证人账户密码  
      --last_block                 用于防止双花，设置当前见证人的最后一笔见证交易的hash, 节点在获得此block后才开始见证

    MISC OPTIONS:               
      --config                     指定配置文件，配置文件必须存在       
```
### 配置文件  
config.json - 位于节点数据目录下，示例如下：
```
    {
        "version": 3,
        "network": 4,
        "node": {
            "io_threads": 8,
            "bg_threads": 4,
            "sync_threads": 4,
            "work_threads": 2
        },
        "rpc": {
            "rpc": "false",
            "rpc_addr": "127.0.0.1",
            "rpc_port": 8765,
            "rpc_control": "false"
        },
        "ws": {
            "ws": "false",
            "ws_addr": "127.0.0.1",
            "ws_port": 8764,
            "ws_control": "false"
        },
        "log": {
            "console": "false",
            "max_size": 16777216,
            "rotation_size": 4194304,
            "flush": "true",
            "verbosity": "info",
            "vmodule": ""
        },
        "p2p": {
            "host": "",
            "port": 30606,
            "max_peers": 25,
            "bootstrap_nodes": [
                "czrnode://927A2362C7CB382E8574D2BD94EC5475D92170B8EBA91D019175185B4FFE4D52@47.34.12.16:30606",
                "czrnode://01CE1577F493C721ED0200A53A3E90C238F897DF0A845DA195C512F37D1D5229@78.65.15.17:30614",
            ],
            "exemption_nodes": [
                "czrnode://01CE1577F493C721ED0200A53A3E90C238F897DF0A845DA195C512F37D1D5229@78.65.15.17:30614"
            ],
            "nat": "true"
        },
        "witness": {
            "witness": "false",
            "witness_account": "",
            "password": "",
            "last_block": ""
        }
    }
```