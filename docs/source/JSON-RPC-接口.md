# RPC接口列表

RPC请求使用HTTP POST方法，请求内容使用JSON格式，其中action字段指定RPC接口名称。

## account_create

  生成账户。rpc_control 需要设置true。

### 请求参数
- action：account_create。
- password：生成账户的密码。
```js
{
    "action": "account_create",
    "password": "s4iH1t@hBFtymA"
}
```
### 返回结果
- code：错误码。0表示成功。  
- msg：错误信息。
- account：生成的账户。    
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "account": "czr_4M943gNHekWpfTmRFJHUYTYV65gnkjN5zAjqTeRTbnNCXfeJrw"
}

//返回失败
{
    "code": 1,
    "msg": "Password can not be empty"
}
```
   
## account_remove
   删除账户。rpc_control 需要设置true。
### 请求参数
- action：account_remove。
- account：删除的账户。
- password：密码。
```js
{
    "action": "account_remove",
    "account": "czr_4M943gNHekWpfTmRFJHUYTYV65gnkjN5zAjqTeRTbnNCXfeJrw",
    "password": "s4iH1t@hBFtymA"
}
```
### 返回结果
- code：错误码。0表示成功。  
- msg：错误信息。 
```js
//返回成功
{
    "code": 0,
    "msg": "OK"
}

//返回失败
{
    "code": 3,
    "msg": "Wrong password"
}
```
   
## account_unlock
   解锁账户。rpc_control 需要设置true。
### 请求参数
- action：account_unlock。
- account：解锁的账户。
- password：密码。
```js
{
    "action": "account_unlock",
    "account": "czr_4M943gNHekWpfTmRFJHUYTYV65gnkjN5zAjqTeRTbnNCXfeJrw",
    "password": "s4iH1t@hBFtymA"
}
```
### 返回结果
- code：错误码。0表示成功。
- msg：错误信息。 
```js
//返回成功
{
    "code": 0,
    "msg": "OK"
}

//返回失败
{
    "code": 3,
    "msg": "Wrong password"
}
```
   
## account_lock
   锁定账户。rpc_control 需要设置true。
### 请求参数
- action：account_lock。
- account：锁定的账户。
```js
{
    "action": "account_lock",
    "account": "czr_4M943gNHekWpfTmRFJHUYTYV65gnkjN5zAjqTeRTbnNCXfeJrw"
}
```
### 返回结果
- code：错误码。0表示成功。   
- msg：错误信息。 
```js
//返回成功
{
    "code": 0,
    "msg": "OK"
}

//返回失败
{
    "code": 2,
    "msg": "Account not found"
}
```
   
## account_import
   导入账户。rpc_control 需要设置true。
### 请求参数
- action：account_import。
- json：导入账户的json。
```js
{
    "action": "account_import",
    "json": "{\"account\":\"czr_3dUnMEsuSiUsKGgfft5VDpM2bX9S6T4ppApHRfn1cBmn2znyEv\",\"kdf_salt\":\"175DCAF994E6992AAD1369014670C086\",\"iv\":\"F6054D9B144A254D3D4EAB78C95F21B6\",\"ciphertext\":\"2A943F3A7316C33B16374D9076FEF5BA7770C2A0424A08501D3663A1467DEDD7\"}"
}
```
### 返回结果
- code：错误码。0表示成功。        
- msg：错误信息。   
- account：导入的账户。     
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "account": "czr_3dUnMEsuSiUsKGgfft5VDpM2bX9S6T4ppApHRfn1cBmn2znyEv"
}

//返回失败
{
    "code": 2,
    "msg": "Invalid json"
}
```
   
## account_export
   导出账户。
### 请求参数
- action：account_export。
- account：导出账户。
```js
{
    "action": "account_export",
    "account": "czr_4GHUc91PYAddCiDHtwFnFDcsQrqdXW58Ps75rpHJsxAnJrQR1d"
}
```
### 返回结果
- code：错误码。0表示成功。  
- msg：错误信息。   
- json：导出账户的json。     
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "json": "{\"account\":\"czr_4GHUc91PYAddCiDHtwFnFDcsQrqdXW58Ps75rpHJsxAnJrQR1d\",\"kdf_salt\":\"37685A5B3413EC419CE4B5B79E0BB020\",\"iv\":\"F046EA90EA24A6CF0CB74BE8C560367B\",\"ciphertext\":\"4A2E6EE4CF04162D2A4DA6116C23CD94487837731055A1BC0FCBDA7E0D7C65A4\"}"
}

//返回失败
{
    "code": 2,
    "msg": "Account not found"
}
```
   
## account_validate
   验证账户格式是否合法。
### 请求参数
- action：account_validate。
- account：验证账户。
```js
{
    "action": "account_validate",
    "account": "czr_4GHUc91PYAddCiDHtwFnFDcsQrqdXW58Ps75rpHJsxAnJrQR1d"
}
```
### 返回结果
- code：错误码。0表示成功。   
- msg：错误信息。   
- valid：验证结果，0：格式不合法，1：格式合法。     
```js
//验证格式不合法
{
    "code": 0,
    "msg": "OK",
    "valid": 0
}
//验证格式合法
{
    "code": 0,
    "msg": "OK",
    "valid": 1
}
```
   
## account_password_change
   修改密码。rpc_control 需要设置true。
### 请求参数
- action：account_password_change。
- account：修改密码的账户。
- old_password：账户原密码。 
- new_password：账户新密码。
```js
{
    "action": "account_password_change",
    "account": "czr_4CGgMNZzmzXKvQx6TrfgSgsbGNSsWsW6FMPv4gQabhZnftrBLC",
    "old_password": "JNVRNHCK2o8N",
    "new_password":"qmwevFcyebqu"
}
```
### 返回结果
- code：错误码。0表示成功。      
- msg：错误信息。    
```js
//返回成功
{
    "code": 0,
    "msg": "OK"
}   

//返回失败
{
    "code": 5,
    "msg": "Wrong old password"
}
```
   
## account_list
   获取当前节点的所有账户。rpc_control 需要设置true。
### 请求参数
- action：account_list。
```js
{
    "action": "account_list"
}
```
### 返回结果
- code：错误码。0表示成功。             
- msg：错误信息。    
```js
//返回成功
{
    "code": 0,
    "msg": "OK"
    "accounts": [
        "czr_356ssGpdDhtjRqKHCP47Rt2mbUwFcFPD3mXT73FJzWEedw3Eog",
        "czr_4qwoBUYAvxgoVq5FHsXCCCkLCVuJ1z4224ZUVZRGhyawuzbWyh"
    ]
}
```
  
## account_block_list
   获取指定账户交易详情。rpc_control 需要设置true。
### 请求参数
- action：account_block_list。
- account：指定查询账户。
- limit：返回交易上限，最大1000。
- index：（可选）当前查询索引，来自返回结果中的next_index，默认为空。
```js
{
    "action": "account_block_list",
    "account": "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u",
    "limit": 100
}
```
### 返回结果
- code：错误码。0表示成功。      
- msg：错误信息。    
- blocks：交易详情列表。[block参数参见交易详情](#block)
- next_index：查询索引, 后续没有数据时为null。
```js
//返回成功
{
    "code": 0,
    "msg": "OK"
    "blocks": [{...}, {...}, ...],
    "next_index": "35EAB31538EBA6CBD8E3FC1C91BFEA425EE13A1CC66B5D650A6FF226B6698A27"
}

//返回失败
{
    "code": 4,
    "msg": "Index not found"
}
```
  
## account_balance
   获取指定账户余额。
### 请求参数
- action：account_balance。
- account：指定的账户。
```js
{
    "action": "account_balance",
    "account": "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u"
}
```
### 返回结果
- code：错误码。0表示成功。       
- msg：错误信息。    
- balance：账户余额。
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "balance": "1000000000000000000" //1CZR
}

//返回失败
{
    "code": 1,
    "msg": "Invalid account"
}
```

## accounts_balances
   获取指定多个账户余额。
### 请求参数
- action：accounts_balances。
- accounts：指定的多个账户。
```js
{
    "action": "accounts_balances",
    "accounts": [
        "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u",
        "czr_4GHUc91PYAddCiDHtwFnFDcsQrqdXW58Ps75rpHJsxAnJrQR1d"
    ]
}
```
### 返回结果
- code：错误码。0表示成功。       
- msg：错误信息。    
- balances：账户余额。
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "balances": {
        "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u": "1000000000000000000", //1CZR
        "czr_4m7NiSx2sBG4Hmdq1Yt6EGKqFQ3rmtBXCsmJZZp4E3pm84LkG9": "1000000000000000000"  //1CZR
    }
}

//返回失败
{
    "code": 1,
    "msg": "Invalid account"
}
```

## account_code
   获取合约账户的代码。
### 请求参数
- action：account_code。
- account：账户。
```js
{
    "action": "account_code",
    "account": "czr_4GHUc91PYAddCiDHtwFnFDcsQrqdXW58Ps75rpHJsxAnJrQR1d"
}
```
### 返回结果
- code：错误码。0表示成功。       
- msg：错误信息。    
- account_code：代码。
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "account_code": "61016B610030600B82828239805160001A6073146000811461002057610022565BFE5B5030600052607381538281F3FE7300000000000000000000000000000000000000003014608060405260043610610052576000357C010000000000000000000000000000000000000000000000000000000090048063DCE4A44714610057575B600080FD5B6100996004803603602081101561006D57600080FD5B81019080803573FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF169060200190929190505050610114565B6040518080602001828103825283818151815260200191508051906020019080838360005B838110156100D95780820151818401526020810190506100BE565B50505050905090810190601F1680156101065780820380516001836020036101000A031916815260200191505B509250505060405180910390F35B6060813B6040519150601F19601F602083010116820160405280825280600060208401853C5091905056FEA165627A7A7230582027C83370D70C11D17B94A12CCB8F7856B88ED68CFC6363465293981CB633B25C0029"
}

//返回失败
{
    "code": 1,
    "msg": "Invalid account"
}
```

## call
  获取合约状态。
### 请求参数
- action：call。
- from：（可选）源账户。
- to：目标账户。 
- data：（可选）合约代码或数据。 
- mci: （可选）string, mci，接受的值："latest", "earliest" 或数字（如:"1352"）, 默认为"latest"。
```js
{
    "action":"call",
    "from":"czr_4kYTyZTjRGQoEioCbT8JcKpDaqjJs2ekpxcucTC14SniuNABi6",
    "to":"czr_3KfLt664eysPMc5pp1wTiRQhYELXM7EruDVoEPYWM4bmZRDZJq",
    "data":"0DBE671F",
    "mci": "earliest"
}
```
### 返回结果
- code：错误码。0表示成功。
- msg：错误信息。
- output：输出结果。    
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "output": "692A70D2E424A56D2C6C27AA97D1A86395877B3A2C6C27AA97D1A86395877B5C"
}

//返回失败
{
    "code": 3,
    "msg": "Invalid to account"
}
```

## estimate_gas
  预估交易需消耗的gas数量。
### 请求参数
- action：estimate_gas。
- from：（可选）源账户。
- to：（可选）目标账户。 
- amount：（可选）string, 金额，单位：10<sup>-18</sup>CZR。
- gas：（可选）string, 执行交易使用的gas上限。
- gas_price：（可选）string, gas价格，单位：10<sup>-18</sup>CZR/gas，手续费 = 实际使用的gas * gas_price。
- data：（可选）智能合约代码或数据。默认为空。 
- mci: （可选）string, mci，接受的值："latest", "earliest" 或数字（如:"1352"）, 默认为"latest"。
```js
{
    "action": "estimate_gas",
    "from": "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u",
    "to": "czr_3dUnMEsuSiUsKGgfft5VDpM2bX9S6T4ppApHRfn1cBmn2znyEv",
    "amount": "1000000000000000000",//1个CZR
    "gas": "21000",
    "gas_price": "1000000000",
    "data": "",
    "mci": "838"
}
```
### 返回结果
- code：错误码。0表示成功。     
- msg：错误信息。
- gas：预估所需消耗的gas。    
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "gas": "21000"
}

//返回失败
{
    "code": 9,
    "msg": "Gas not enough or excute fail"
}
```

## logs
  获取智能合约产生的event log。
### 请求参数
- action：logs
- from_stable_block_index：（可选）开始搜索的stable block index，默认为0。
- to_stable_block_index：（可选）结束搜索的stable block index，默认为last stable block index。 
- account：（可选）搜索的账号，默认为空。
- topics：（可选）搜索的topic数组，采用or逻辑，默认为空。
```js
{
    "action": "logs",
    "account": "czr_3DG8FjYSAqkBNubcSVAAjAtSQ9Q2tWVNwPS8VHQ55XwWG4DsTS",
    "topics":[ "260823607ceaa047acab9fe3a73ef2c00e2c41cb01186adc4252406a47d73446" ]
}
```
### 返回结果
- code：错误码。0表示成功。     
- msg：错误信息。
- logs：log数组。    
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "logs": [
        {
            "address": "czr_3DG8FjYSAqkBNubcSVAAjAtSQ9Q2tWVNwPS8VHQ55XwWG4DsTS",
            "data": "0000000000000000000000000000000000000000000000000000000000000000",
            "topics": [
                "260823607ceaa047acab9fe3a73ef2c00e2c41cb01186adc4252406a47d73446"
            ]
        },
        {
            "address": "czr_3DG8FjYSAqkBNubcSVAAjAtSQ9Q2tWVNwPS8VHQ55XwWG4DsTS",
            "data": "0000000000000000000000000000000000000000000000000000000000000001",
            "topics": [
                "260823607ceaa047acab9fe3a73ef2c00e2c41cb01186adc4252406a47d73446"
            ]
        }
    ]
}

//返回失败
{
    "code": 3,
    "msg": "Invalid account"
}
```

## send_block
  发送交易。enable_control 需要设置true。
### 请求参数
- action：send_block。
- previous：（可选）源账户的上一笔交易hash。可用于替换无法被打包的交易。
- from：源账户。
- to：目标账户。 
- amount：string, 金额，单位：10<sup>-18</sup>CZR。
- password：源账户密码。
- gas：string, 执行交易使用的gas上限。未使用完的部分会返回源账户。
- gas_price：string, gas价格，单位：10<sup>-18</sup>CZR/gas，手续费 = 实际使用的gas * gas_price。
- data：（可选）智能合约代码或数据。默认为空。 
```js
{
    "action": "send_block",
    "from": "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u",
    "to": "czr_3dUnMEsuSiUsKGgfft5VDpM2bX9S6T4ppApHRfn1cBmn2znyEv",
    "amount": "1000000000000000000",//1个CZR
    "password": "12345678",
    "gas": "21000",
    "gas_price": "1000000000",
    "data": ""
}
```
### 返回结果
- code：错误码。0表示成功。     
- msg：错误信息。
- hash：交易hash。    
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "hash": "CDE1EC247CAC41C321024DCEBF065662A46A49A119EF0641C0547111FBCB315D"
}

//返回失败
{
    "code": 10,
    "msg": "Wrong password"
}
```
    
## generate_offline_block
  生成未签名的交易，返回交易详情。rpc_control 需要设置true。
### 请求参数
- action：generate_offline_block。
- previous：（可选）源账户的上一笔交易hash。可用于替换无法被打包的交易。
- from：源账户。
- to：目标账户。 
- amount：string, 金额，单位：10<sup>-18</sup>CZR。
- gas：string, 执行交易使用的gas上限。未使用完的部分会返回源账户。
- gas_price：string, gas价格，单位：10<sup>-18</sup>CZR/gas，手续费 = 实际使用的gas * gas_price。
- data：（可选）智能合约代码或数据，默认为空。 
```js
{
	"action": "generate_offline_block",
	"from": "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u",
	"to": "czr_3w6RT4KJ5CGocZRUqwuxUfUciLggCTAgpccLrMwxqgJuSB2iW6",
	"amount": "1000000000000000000",
	"gas": "21000",
	"gas_price": "1000000000",
	"data": ""
}
```
### 返回结果
- code：错误码。0表示成功。   
- msg：错误信息。
- hash：交易哈希。  
- previous：源账户的上一笔交易。  
- from：源账户。
- to：目标账户。 
- amount：string, 金额，单位：10<sup>-18</sup>CZR。
- gas：string, 执行交易使用的gas上限。未使用完的部分会返回源账户。
- gas_price：string, gas价格，单位：10<sup>-18</sup>CZR/gas，手续费 = 实际使用的gas * gas_price。
- data：参见输入参数。   
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "hash": "D6FB0D0F3D56F5B5D7C4B4D95D73701A341C68A92495D259B9836488CB60C383",
    "from": "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u",
    "to": "czr_3dUnMEsuSiUsKGgfft5VDpM2bX9S6T4ppApHRfn1cBmn2znyEv",
    "amount": "1000000000000000000",
    "previous": "0000000000000000000000000000000000000000000000000000000000000000",
    "gas": "21000",
    "gas_price": "1000000000",
    "data": ""
}

//返回失败
{
    "code": 5,
    "msg": "Invalid gas format"
}
```

## send_offline_block
  发送已签名交易，请求参数来自接口[generate_offline_block](#generate_offline_block),返回交易哈希。rpc_control 需要设置true。
### 请求参数
- action：send_offline_block。
- previous：源账户的上一笔交易hash。
- from：源账户。
- to：目标账户。 
- amount：string, 金额，单位：10<sup>-18</sup>CZR。
- gas：string, 执行交易使用的gas上限。未使用完的部分会返回源账户。
- gas_price：string, gas价格，单位：10<sup>-18</sup>CZR/gas，手续费 = 实际使用的gas * gas_price。
- data：（可选）智能合约代码或数据，默认为空。    
- signature：交易签名。
```js
{
	"action": "send_offline_block",
	"previous": "0000000000000000000000000000000000000000000000000000000000000000",
	"from": "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u",
	"to": "czr_3w6RT4KJ5CGocZRUqwuxUfUciLggCTAgpccLrMwxqgJuSB2iW6",
	"amount": "1000000000000000000",
	"gas": "21000",
	"gas_price": "1000000000",
	"data": "",
	"signature": "71408627FF461C9DE076A38B71953A3045C95D1E1E841A2224E4AC3E503C0D0046FE8FEEB6E72B257B7743F53AFEC1CE80699D5E125C60794D6D09823C3B1E0C"
}
```
### 返回结果
- code：错误码。0表示成功。         
- msg：错误信息。        
- block：交易详情。    
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "hash": "93B7A0ECCE8D23E6E1969FAA5B4326CEDA78032EEB44B5F85A26AFFA84F50D64"
}

//返回失败
{
    "code": 1,
    "msg": "Invalid from account"
}
```
   
## sign_msg
  签名消息。
### 请求参数
- action：sign_msg。
- public_key：签名公钥。
- password：公钥密码。   
- msg：签名的消息。 
```js
{
    "action":"sign_msg",
    "public_key": "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u",
    "password":"s4iH1t@hBFtymA",
    "msg":"CB09A146D83668AE13E951032D2FD94F893C9A0CA0822ED40BBE11DC0F167D1B"
}
```
### 返回结果
- code：错误码。0表示成功。  
- msg：错误信息。
- hash：交易hash。    
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "signature": "E09CDD795E6959C3B85FDCA0EA56BCFBBC7BE05A0D0AB6B1A0C6DD23FF0AA36F635C70CB731DAC07909A572132128120EBC12862D4BEC2FE70E9A6060F32CA0C"
}

//返回失败
{
    "code": 10,
    "msg": "Wrong password"
}
```

## block
  获取交易详情。
### 请求参数
- action：block。
- hash：交易哈希。 
```js
{
    "action":"block",
    "hash": "412254AB895FD2E6ADE6F9076CA8297516F2845C989A13AC008CD5D70157AFFB"
}
```
### 返回结果
- code：错误码。0表示成功。    
- msg：错误信息。
- block：交易详情，如果不存在，则为null。 
  - hash：交易hash。    
  - type：类型，0：创世交易，1：见证交易，2：普通交易。    
  - from：源账户。
  - content: block内容，各类型内容如下：
    - 创世交易：
      - to：目标账户。
      - amount：金额，单位：10<sup>-18</sup>CZR。
      - data_hash：data计算的hash。
      - data：智能合约代码或数据。
      - timestamp：时间戳。    
    - 见证交易：
      - previous：源账户的上一笔交易，账户第一笔交易previous为全0的hash值。
      - parents：DAG图上的父交易列表。
      - links：见证交易连接的普通交易列表
      - last_stable_block：本次交易的最后一个稳定的交易 
      - last_summary_block：本次交易最优父交易的last_stable_block。 
      - last_summary：last_summary_block对应的summary。
      - timestamp：时间戳。    
    - 普通交易：
      - to：目标账户。   
      - amount：金额，单位：10<sup>-18</sup>CZR。
      - previous：源账户的上一笔交易，账户第一笔交易previous为全0的hash值。
      - gas：string, 执行交易使用的gas上限。未使用完的部分会返回源账户。
      - gas_price：string, gas价格，单位：10-18CZR/gas，手续费 = gas_used * gas_price。
      - data_hash：data计算的hash。   
      - data：智能合约代码或数据。            
  - signature：签名。    
```js
//返回成功

//见证交易
{
    "code": 0,
    "msg": "OK",
    "block": {
        "hash": "312254FF897CA2E6ADE6F99EDAA829751481845C555A13AC008AB5D70157AEED",
        "type": 1,
        "from": "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u",
        "content": {
            "previous": "A5E40538D4FA7505DDE81C538AAAB97142312E3FE3D606901E2C439967FE10F0",
            "parents": [
                "16501EAE48B973F73CDAE418E4BD4F852EE8D11337CD9B081FF70D7FD9602283",
                "AC27E98BCF2D322E36AD65561E1B65D19D31DC7695D6A243F46F25A8769DBA16"
            ],
            "links": [
                "8992AE96EE14A6138CF7E35D9EFB745751BCFA3EFA22D9032EBCC23CEDE2AA1C",
                "FFE2606553075B034889E26D25FF368394C8A2FBEE7F8429AA4AEB5BD6F48EEB"
            ],
            "last_stable_block:": "4C7F88CC9308B7A6050E6B67011C418B04BB67D5702BA43027BC1CA41BF052AD",
            "last_summary_block": "77D3DE09B6418A5E28070EEB504BD84F493DD6044D2FB6DEA6260470F652EE41",
            "last_summary:": "1E1A13B26AA4309DA058036A31EA5B14AC1BF227FA416844A0E34A52F20FE542",
            "timestamp": 1526568538,
        },
        "signature": "853F9A8B9F99A8056D04AB93A03532AB7BDD164376C954FEAFCEFED698255D38984A41E1A4788C595EF83C29964DDE4E2ADEB3A21AB63E95497323FB8C9F5D03",
    }
}

//普通交易
{
    "code": 0,
    "msg": "OK",
    "block": {
        "hash": "412254AB895FD2E6ADE6F9076CA8297516F2845C989A13AC008CD5D70157AFFB",
        "type": 2,
        "from": "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u",
        "content": {
            "to": "czr_4k1FXs5xvfYcKiikFeV3GtyMRqYMwbjatL5YVURqYf1KBgC8Mq",
            "amount": "1000000000000000000", //1CZR
            "previous": "A5E40538D4FA7505DDE81C538AAAB97142312E3FE3D606901E2C439967FE10F0",
            "gas": "21000",
            "gas_price": "1000000000"
            "data_hash": "EF27E98EBD2D322E68E965561E1B65D19D31FDA595D6A243F46F57A8769DAA90",
            "data": "496E204D617468205765205472757374"
        },
        "signature": "853F9A8B9F99A8056D04AB93A03532AB7BDD164376C954FEAFCEFED698255D38984A41E1A4788C595EF83C29964DDE4E2ADEB3A21AB63E95497323FB8C9F5D03",
    }
}

//返回失败
{
    "code": 1,
    "msg": "Invalid hash format"
}
```

## blocks
  批量获取交易详情。
### 请求参数
- action：blocks。
- hashs：交易哈希列表。不存在的hash对应结果null。
```js
{
    "action": "blocks",
    "hashes": [
        "412254AB895FD2E6ADE6F9076CA8297516F2845C989A13AC008CD5D70157AFFB",
        "B222C88AB9729B4DEF3F5E12962DB12A2FA80C9B50A4003CD67CE024428DAC61"
    ]
}
```
### 返回结果
- code：错误码。0表示成功。      
- msg：错误信息。
- blocks：交易详情列表。[block参数参见交易详情](#block)    
```js
//返回成功
{
    "code": "0",
    "msg": "OK",
    "blocks": [{...}, {...}, ...]
}

//返回失败
{
    "code": 1,
    "msg": "Invalid hash format"
}
```

## block_state
  获取交易状态详情。
### 请求参数
- action：block_state。
- hash：交易哈希。 
```js
{
    "action":"block_state",
    "hash": "412254AB895FD2E6ADE6F9076CA8297516F2845C989A13AC008CD5D70157AFFB"
}
```
### 返回结果
- code：错误码。0表示成功。    
- msg：错误信息。
- block_state：交易状态详情，如果不存在，则为null。    
  - hash：交易hash。    
  - type：类型, 0：创世交易，1：见证交易，2：普通交易。  
  - content：block state 内容，各类型内容如下：
    - 创世交易：
      - level: 交易级别。
      - witnessed_level：见证级别。
    - 见证交易：
      - level: 交易级别。
      - witnessed_level：见证级别。
      - best_parent：最优父单元。
    - 普通交易： 
      - level: 交易级别。
  - is_stable：是否稳定, 0：不稳定，1：稳定。
  - stable_content：稳定内容，当不稳定时为null
    - status：确认状态，0：成功，1：双花，2：无效，3：智能合约执行失败。 
    - stable_index：稳定的index，表示稳定后的全局顺序，从0开始递增。
    - mc_timestamp：主链时间。 
    - stable_timestamp：稳定时间。
    - mci：主链index。
    - 各类型不同的stable_content属性：
      - 创世交易：
        - is_free：是否有子交易。
        - is_on_mc：是否在主链上。
        - from_state: from账号状态hash
        - to_states：交易产生的其他账号的新状态hash列表
        - gas_used：交易执行实际消耗的gas数量。
        - log：交易执行日志。
        - log_bloom：交易执行日志的Bloom过滤器值。
      - 见证交易：
        - is_free：是否有子交易。
        - is_on_mc：是否在主链上。
      - 普通交易：
        - from_state: from账号状态hash。status等于1或2时为null。
        - to_states：交易产生的其他账号的新状态hash列表。status等于1或2时为null。
        - gas_used：交易执行实际消耗的gas数量。status等于1或2时为null。
        - log：交易执行日志。status等于1或2时为null。
        - log_bloom：交易执行日志的Bloom过滤器值。status等于1或2时为null。
        - contract_account：如果交易为创建合约的交易，则返回新建的合约地址，否则为null。
```js
//返回成功

//见证交易
{
    "code": 0,
    "msg": "OK",
    "block_state": {
        "type": 1,
        "content": {
            "level": 245,
            "witnessed_level": 224,
            "best_parent": "16501EAE48B973F73CDAE418E4BD4F852EE8D11337CD9B081FF70D7FD9602283"
        },
        "is_stable": 1,
        "stable_content": {
            "status": 0,
            "stable_index": 3638,
            "mc_timestamp": 1526568538,
            "stable_timestamp": 1526568543,
            "mci": 3155,
            "is_on_mc": 1,
            "is_free": 0
        }
    }
}

//普通交易
{
    "code": 0,
    "msg": "OK",
    "block_state": {
        "type": 2,
        "content": {
            "level": 21
        },
        "is_stable": 1,
        "stable_content": {
            "status": 0,
            "stable_index": 3638,
            "mc_timestamp": 1526568538,
            "stable_timestamp": 1526568543,
            "mci": 3155,
            "from_state": "DF27E98aBD2D322E688836561E1B65D19D31FDE215D6A243F46F57A8769DBB87",
            "to_states": ["412254AB895FD2E6ADE6F9076CA8297516F2845C989A13AC008CD5D70157AFFB"],
            "gas_used": 21000,
            "log": [],
            "log_bloom": "0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
            "contract_account": null 
        }
    }
}

//返回失败
{
    "code": 1,
    "msg": "Invalid hash format"
}
```

## block_states
  批量获取交易状态。
### 请求参数
- action：blocks。
- hashs：交易状态哈希列表。不存在的hash对应结果null。
```js
{
    "action": "block_states",
    "hashes": [
        "412254AB895FD2E6ADE6F9076CA8297516F2845C989A13AC008CD5D70157AFFB",
        "B222C88AB9729B4DEF3F5E12962DB12A2FA80C9B50A4003CD67CE024428DAC61"
    ]
}
```
### 返回结果
- code：错误码。0表示成功。      
- msg：错误信息。
- blocks：交易详情列表。[block_state参数参见交易详情](#block_state)    
```js
//返回成功
{
    "code": "0",
    "msg": "OK",
    "block_states": [{...}, null, {...}, ...]
}

//返回失败
{
    "code": 1,
    "msg": "Invalid hash format"
}
```

## block_traces
  获取智能合约内部交易trace列表。
### 请求参数
- action：block_traces。
- hash：交易哈希。 
```js
{
    "action":"block_traces",
    "hash": "412254AB895FD2E6ADE6F9076CA8297516F2845C989A13AC008CD5D70157AFFB"
}
```
### 返回结果
- code：错误码。0表示成功。    
- msg：错误信息。
- block_traces：交易trace列表。
  - 单个交易trace属性：
    - type：类型，0：call，1：create，2：suicide。
    - action：不同类型内容如下：
      - call:
        - call_type：call类型。
        - from: 源账号。
        - to：目标账号。
        - gas：string，gas限制。
        - data：输入数据。
        - amount：string，金额，单位：10<sup>-18</sup>CZR。
      - create：
        - from: 源账号。
        - gas：string，gas限制。
        - init：创建合约的代码。
        - amount：string，金额，单位：10<sup>-18</sup>CZR。
      - suicide：
        - contract_account：合约地址。
        - refund_account：退款账号。
        - balance：退款余额。
    - result：不同类型内容如下，当合约执行出错时，没有此属性：
      - call：
        - gas_used：使用的gas。
        - output：输出数据。
      - create：
        - gas_used：使用的gas。
        - contract_account: 新建合约的地址。
        - code：新建合约的代码。
      - suicide：result为null      
    - error: 错误消息，当合约执行没有出错时，没有此属性。
    - subtraces：子trace个数。
    - trace_address：trace层次位置。  
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "block_traces": [{
        "type": 0,  //call
        "action": {
            "call_type": "call",
            "from": "czr_4iig3fTcXQmz7bT2ztJPrpH8usrqGTN5zmygFqsCJQ4HgiuNvP",
            "to": "czr_33EuccjKjcZgwbHYp8eLhoFiaKGARVigZojeHzySD9fQ1ysd7u",
            "gas": "25000",
            "data": "",
            "amount": "120000000000000000000"
        },
        "result": {
            "gas_used": "21000",
            "output": "",
        },
        "subtraces":0,
        "trace_address": []
    }, ...]
}

//返回失败
{
    "code": 1,
    "msg": "Invalid hash format"
}
```

## stable_blocks
  获取已稳定的指定mci下的多笔交易。
### 请求参数
- action：stable_blocks。 
- limit：返回交易上限，最大1000。  
- index：（可选）第一个block的stable_index，可取结果中的next_index，默认为0。 
```js
{
    "action": "stable_blocks",
    "limit": 100,
    "index": 15577
}
```
### 返回结果
- code：错误码。0表示成功。    
- msg：错误信息。
- blocks：交易详情列表。[block参数参见交易详情](#block)  
- next_index：下一个block的stable_index，后续没有数据时为null。 
```js
//返回成功
{
    "code": "0",
    "msg": "OK",
    "blocks": [{...}, {...}, ...],
    "next_index": 15677
}

//返回失败
{
    "code": 1,
    "msg": "Invalid hash format"
}
```

## status
  获取当前状态。
### 请求参数
- action：status。  
```js
{
    "action": "status"
}
```
### 返回结果
- code：错误码。0表示成功。        
- msg：错误信息。
- syncing: 是否同步中，0：未同步，1：同步中。
- last_stable_mci：最大稳定主链index。  
- last_mci：最大主链index。  
- last_stable_block_index：最大稳定交易的index, 稳定交易的index从0开始依次递增，表示每笔交易稳定后的全局顺序
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "syncing": 0,
    "last_stable_mci": 360,
    "last_mci": 376,
    "last_stable_block_index": 48367
}
```

## witness_list
  获取见证人列表。
### 请求参数
- action：witness_list。  
```js
{
    "action": "witness_list"
}
```
### 返回结果
- code：错误码。0表示成功。      
- msg：错误信息。
- witness_list：见证人列表。   
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "witness_list": [
        "czr_321JDA7Brgbnm64iY2Xh8yHMEqEgBDutnoTKVLcxW2DJvJLUsS",
        "czr_32RmC9FsxjgLkgRQ58j3CdLg79cQE3KaY2wAT1QthBTU25vpd3",
        "czr_3MnXfV9hbmxVPdgfrPqgUiH6N7VbkSEhn5VqBCzBcxzTzkEUxU",
        "czr_3SrfL6LnPbtyf6sanrgtKs1BTYDN8taacGBVG37LfZVqXvRHbf",
        "czr_3igvJpdDiV4v5HxEzCifFcUpKvWsk3qWYNrTrbEVQztKbpyW1z",
        "czr_3tiy2jgoUENkszPjrHjQGfmopqwV5m9BcEh2Grb1zDYgSGnBF7",
        "czr_47E2jJ9rXVk5GRBcTLQMLQHXqsrnVcV5Kv2CWQJ6dnUaugnvii",
        "czr_49BvoaSgGnyfPdaHfrSdac74fcxV4cUdysskHSQPQ8XisShN3P",
        "czr_4HhYojuHanxQ57thkSxwy5necRtDFwiQP7zqngBDZHMjqdPiMS",
        "czr_4MYTD6Xctkb6fEL8xUZxUwY6eqYB7ReEfB61YFrMHaZxsqLCKd",
        "czr_4URkteqck9rM8Vo6VzWmvKtMWoSH8vo4A1rADNAFrQHxAR23Tb",
        "czr_4ZJ8hBdR6dLv4hb1RPCmajdZf7ozkH1sHU18kT7xnXj4mjxxKE",
        "czr_4aBXjWXyN7WVGqMKH7FgnSoN9oePeEPiZsrtc2AMYyuTRJoNpb",
        "czr_4iig3fTcXQmz7bT2ztJPrpH8usrqGTN5zmygFqsCJQ4HgiuNvP"
    ]
}
```

## version
  获取当前节点后台程序版本号，rpc版本号，数据库版本号。
### 请求参数
- action：version。  
```js
{
    "action": "version"
}
```
### 返回结果
- code：错误码。0表示成功。        
- msg：错误信息。  
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "version": "0.9.7",
    "rpc_version": "1",
    "store_version": "4"
}
```

## debug_trace_transaction
  交易调试接口。返回交易的操作码(opcode)和执行时的堆栈和内存信息。
### 请求参数
- action: debug_trace_transaction。
- hash: 交易哈希值。
- options: （可选）执行交易追踪时的选项。包括 disable_storage(默认值为true)和disable_memory，disable_stack，full_storage（默认值为false)。
```js
{
    "action": "debug_trace_transaction",
    "hash": "9E11690B3B1CB015646ECC549A746B25E08D791E32D38363A905F2A3315C2CC1",
    "options": {
    	"disable_storage": false
    }
}
```
### 返回结果
- code：错误码。0表示成功。  
- msg：错误信息。
- gas：string, 执行交易使用的gas上限。
- return_value： 执行交易所返回的值。
- struct_logs：交易执行的追踪记录。    
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "gas": "1000000",
    "return_value": "0x",
    "struct_logs": [
        {
            "stack": [],
            "memory": [],
            "storage": {
                "0x00": "0000000000000000000000000000000000000000000000000000000000000064"
            },
            "op": "PUSH1",
            "pc": "0",
            "gas": "978536",
            "gasCost": "3",
            "depth": "1"
        },
        {
            "stack": [
                "0000000000000000000000000000000000000000000000000000000000000080"
            ],
            "op": "PUSH1",
            "pc": "2",
            "gas": "978533",
            "gasCost": "3",
            "depth": "1"
        },
        ......
//返回失败
{
    "code": 1,
    "msg": "Invalid hash"
}
```

## debug_storage_range_at
  获取合约账户执行某一交易后的存储数据。
### 请求参数
- action: debug_storage_range_at。
- hash: 交易hash值。
- account: 需要调试的账户。
- begin: 获取存储数据的开始地址。
- max_results: 获取数据的上限值，仅显示max_results以内的记录。
```js
{
    "action": "debug_storage_range_at",
    "hash": "9E11690B3B1CB015646ECC549A746B25E08D791E32D38363A905F2A3315C2CC1",
    "account": "czr_4AMgTgyCdzjJCayjyELXgiSqQHiyCXjmCKN174Tiku5jUdGxp5",
    "begin": "0000000000000000000000000000000000000000000000000000000000000000",
    "max_results": 100
}
```
### 返回结果
- code：错误码。0表示成功。  
- msg：错误信息。
- next_key：存储数据超过max_results之外的第一条记录的键值。
- storage：合约的存储数据
```js
//返回成功
{
    "code": 0,
    "msg": "OK",
    "next_key": "0x00c26d91c2b89c096a024093917ff4e8e78485a5199fdc264f198be4a34119fc",
    "storage": {
        "0x290decd9548b62a8d60345a988386fc84ba6bc95484008f6362f93160ef3e563": {
            "key": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "value": "0x0000000000000000000000000000000000000000000000000000000000000064"
        ......
        }
    }
}
//返回失败
{
    "code": 1,
    "msg": "Invalid hash"
}
```
