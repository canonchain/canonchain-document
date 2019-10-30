# Command line interface

```
    $ canonchain --help
    NAME:
       canonchain - the canonchain command line interface

    USAGE:
       canonchain command [command options] [arguments...]
       
    VERSION:
       1.0-stable

    COMMANDS:
      --account_create             Create a new account
      --account_remove             Remove account
        arguments：
          --account                  Account
      --account_import             Import an existing account
        arguments：
          --file                     Account json file
      --account_list               List all accounts in the node
      --daemon                     Start node daemon
      --help                       Show help information
      --version                    Show version number

    NODE OPTIONS:
      --data_path                  Use the supplied path as the data directory
      --io_threads                 Number of IO threads
      --bg_threads                 Number of back-end threads
      --sync_threads               Number of syncing threads
      --work_threads               Number of CPU threads to use for calculating work

    RPC OPTIONS:
      --rpc                        Enable the HTTP-RPC server
      --rpc_addr                   HTTP-RPC server listening address (default: 127.0.0.1)
      --rpc_port                   HTTP-RPC server listening port (default: 8765)
      --rpc_control                Enable the HTTP-RPC write permission

    WS OPTIONS:
      --ws                         Enable the WS-RPC server  
      --ws_addr                    WS-RPC server listening address (default: 127.0.0.1)
      --ws_port                    WS-RPC server listening port (default: 8764)
      --ws_control                 Enable the WS-RPC write permission

    LOG OPTIONS:
      --console                    Error info output to console
      --max_size                   The maximum total size of rotated file
      --rotation_size              The size of the file at which rotation should occur 
      --flush                      Automatically flush the file after each written record    
      --verbosity                  Logging verbosity: none,error,warning,info,debug,trace (default: info)
      --vmodule                    Per-module verbosity: comma-separated list of <module>=<level> (all module list:node,p2p,rpc,pow,sync）

    P2P OPTIONS:
      --host                       P2P监听地址 (默认: 127.0.0.1)
      --port                       P2P监听端口 (默认: 30606) 
      --max_peers                  最大Peer数 (默认: 25)  
      --bootstrap_nodes            引导节点 
      --exemption_nodes            豁免惩罚节点 
      --nat                        开启NAT穿透

    OPENCL OPTIONS:                
      --opencl                     开启OpenCL   
      --platform                   Platform
      --device                     Device
      --opencl_threads             OpenCL线程数

    WITNESS OPTIONS:               
      --witness                    开启见证人模式       
      --witness_account            见证人账户或者账户文件//账户:czr_3MnXfV9hbmxVPdgfrPqgUiH6N7VbkSEhn5VqBCzBcxzTzkEUxU 或账户文件:F:/czr_latest/test/czr_3MnXfV9hbmxVPdgfrPqgUiH6N7VbkSEhn5VqBCzBcxzTzkEUxU.json
      --password                   见证人账户密码  
      --last_block                 见证人上次发送的交易哈希 

    MISC OPTIONS:               
      --config                     指定配置文件，配置文件必须存在       
```
### 配置文件  
config.json - 位于节点数据目录下，示例如下：
```
    {
        "version": "2",
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
        "opencl": {
            "opencl": "false",
            "platform": 0,
            "device": 0,
            "threads": 1048576
        },
        "witness": {
            "witness": "false",
            "witness_account": "",
            "password": "",
            "last_block": ""
        }
    }
```