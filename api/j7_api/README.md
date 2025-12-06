# **J7_omnixep_server – API Documentation**

**J7_omnixep_server** is part of the **oxep_services** suite.  
It exposes REST API endpoints to interact with Electra Protocol (XEP), OmniXEP Layer-2 tokens, NFTs, UTXO state, raw transactions, and blockchain statistics.

---

# 📌 **Table of Contents**

### **1. API Endpoints**
- [Network Stats](#network-stats)  
- [Address Endpoints](#address-endpoints)  
- [Transactions](#transactions)  
- [Blocks](#blocks)  
- [OmniXEP Contracts](#omnixep-contracts)  
- [Token & NFT Raw Transactions](#token--nft-raw-transactions)  
- [UTXO State](#utxo-state)  
- [NFT (Single Item)](#nft-single-item)  
- [Recent Data](#recent-data)

### **2. Endpoint Details**

---

# **1. API Endpoints**

## **Network Stats**
- **GET** [/api/v2/networkstats](#get-apiv2networkstats)

## **Address Endpoints**
- **GET** [/api/v2/address/\<ADDRESS\>/transactions](#get-apiv2addressaddresstransactions)
- **GET** [/api/v2/address/\<ADDRESS\>/balances](#get-apiv2addressaddressbalances)
- **GET** [/api/v2/address/\<ADDRESS\>/utxos](#get-apiv2addressaddressutxos)
- **GET** [/api/v2/omnixep/address/\<ADDRESS\>/nfts](#get-apiv2omnixepaddressaddressnfts)

## **Transactions**
- **GET** [/api/v2/transaction/\<TXID\>](#get-apiv2transactiontxid)

## **Blocks**
- **GET** [/api/v2/block/\<BLOCK\>](#get-apiv2blockblock)

## **OmniXEP Contracts**
- **GET** [/api/v2/omnixep/contracts/updateindex](#get-apiv2omnixepcontractsupdateindex)
- **GET** [/api/v2/omnixep/contracts](#get-apiv2omnixepcontracts)
- **GET** [/api/v2/omnixep/contracts/\<PID\>](#get-apiv2omnixepcontractspid)

## **Token & NFT Raw Transactions**
- **POST** [/api/v2/omnixep/rawsendtoken](#post-apiv2omnixeprawsendtoken)  
- **POST** [/api/v2/omnixep/rawsendnft](#post-apiv2omnixeprawsendnft)  
- **POST** [/api/v2/omnixep/rawminttoken](#post-apiv2omnixeprawminttoken)  
- **POST** [/api/v2/omnixep/rawmintnft](#post-apiv2omnixeprawmintnft)  
- **POST** [/api/v2/sendrawtransaction](#post-apiv2sendrawtransaction)  

## **UTXO State**
- **GET** [/api/v2/utxos](#get-apiv2utxos)

## **NFT (Single Item)**
- **GET** [/api/v2/omnixep/nft/\<PID\>/\<ID\>](#get-apiv2omnixepnftpidid)

## **Recent Data**
- **GET** [/api/v2/lasttransactions](#get-apiv2lasttransactions)  
- **GET** [/api/v2/lastblocks](#get-apiv2lastblocks)  

---

# **2. Endpoint Details**

---

## <a name="network-stats"></a>**GET /api/v2/networkstats**

Returns global blockchain status.

```js
{
  "error": null,
  "data": {
    "supply": "18,308,243,410.57028961",    // current circulating supply
    "last_block": "1,934,900",              // last valid block 
    "nodes": "335",                         // current nodes connected to the seed
    "contracts": "274",                     // count of valid OmniXEP contracts
    "utxos": "1,979,123"                    // current valid UTXO set
  }
}
```

---

## **GET /api/v2/address/\<ADDRESS\>/transactions**

Returns the transactions list for `<ADDRESS>` (Contract ID filter option)

Query parameters:

| Parameter | Default | Description |
|----------|---------|-------------|
| pid      | NONE      | Contract PID (0 = XEP) |
| page     | 1       | Page number |
| count    | 100     | Items per page |

```js
{
  "error": null,
  "data": [
    {
        // XEP tx, pid = 0
            "amount_pid": 0,
            "amount_xep": 10000000,
            "block": 1877766,
            "block_hash": "30066ef1bc3f3e9a79949b7e84d608d58e8ef9d9e2203038afd3f82eee15a5b1",
            "body": "",
            "data_content": "",
            "data_type": 4,
            "decimals": true,
            "header": "",
            "invalid_reason": "",
            "l2_fee": 0,
            "layer": "XEP",
            "pid": 0,
            "recipient": {
                "xKutgZdyAPAnHrYE5APQ8NQPBK7DwgWgi6": 10000000
            },
            "sender": [
                "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP"
            ],
            "timestamp": 1759238464,
            "token_end": 0,
            "token_start": 0,
            "trade_pid_1": 0,
            "trade_pid_2": 0,
            "txid": "ca5aadaa9f0ef08013bd86e773f2aa1d79135553c03930881702bd21d3f5fe44",
            "type": 306,
            "type_str": "[TRANSFER]",
            "valid": true,
            "xep_fee": 54000
        },
        // OmniXEP tx, pid > 2
        {
            "amount_pid": 100000000,
            "amount_xep": 0,
            "block": 1831327,
            "block_hash": "e0accaf13dbf16fc3bb50bb51be3d78a2357b0f5192a2006e3fd4c424d31e519",
            "body": "%1 1.00000000 tokens",
            "data_content": "",
            "data_type": 4,
            "decimals": true,
            "header": "#113",
            "invalid_reason": "",
            "l2_fee": 54000,
            "layer": "OMNIXEP",
            "pid": 113,
            "recipient": "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP",
            "sender": "xHmJQA3tx6FGq29S6Haa7bpyCzUeapJVQm",
            "timestamp": 1755504000,
            "token_end": 0,
            "token_start": 0,
            "trade_pid_1": 0,
            "trade_pid_2": 0,
            "txid": "f1bbc360a5bb30f58fceeda7aaa7cd3a8b6dcdaa7e061776675b3c6ede479fde",
            "type": 0,
            "type_str": "[TOKEN TRANSFER]",
            "valid": true,
            "xep_fee": 34200
        },
        ...
  ]
}
```

---

## **GET /api/v2/address/\<ADDRESS\>/balances**

Returns the multi layer balances for `<ADDRESS>`, XEP is always at position [0]

```js
{
  "error": null,
  "data": {
    "address": "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP",
    "balances": [
        {
            "balance": 1393431020,
            "decimals": true,
            "frozen": 0,
            "is_nft": false,
            "property_id": 0,
            "reserved": 0,
            "total": 1393431020
        },
        {
            "balance": 39350000000,
            "decimals": true,
            "frozen": 0,
            "is_nft": false,
            "property_id": 9,
            "reserved": 0,
            "total": 39350000000
        },
        ...
    ]
  }
}
```

---

## **GET /api/v2/address/\<ADDRESS\>/utxos**

Returns the existing UTXOs for `<ADDRESS>`

```js
{
  "error": null,
  "data": [
        {
            "address": "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP",
            "coinbase": false,
            "height": 1759918,
            "outputIndex": 0,
            "satoshis": 20000000,
            "script": "a914f8f136b5a4c0f66770363a86ec00bbbc640bf7c187",
            "txid": "ea5e1d0884ba5f3d3ff59ba6ec7483f68067f4c20fd004974dc6f6c5c9d30cf1"
        },
        {
            "address": "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP",
            "coinbase": false,
            "height": 1780919,
            "outputIndex": 0,
            "satoshis": 100000000,
            "script": "a914f8f136b5a4c0f66770363a86ec00bbbc640bf7c187",
            "txid": "f7116eeae5321f4e295d94a0c4783243ac1e9e050ded22ac4c08a91966cf25fe"
        },
        ...
  ]
}
```

---

## **GET /api/v2/omnixep/address/\<ADDRESS\>/nfts**

Returns the NFTs owned by `<ADDRESS>` (Contract ID filter option)

Query parameters:

| Parameter | Default | Description |
|----------|---------|-------------|
| pid      | NONE       | If provided, PID must be a valid NFT contract |
| page     | 1       | Page number |
| count    | 100     | Items per page |

```js
{
  "error": null,
  [
        {
            "grant_data": "random text",
            "grant_type": 4,
            "holder_data": "",
            "holder_type": 4,
            "index": 15,
            "issuer_data": "",
            "issuer_type": 4,
            "owner": "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP",
            "pid": 70
        },
        {
            "grant_data": "{\n    \"db_account\": 1,\n    \"db_assets\": 1,\n    \"db_nft\": 1,\n    \"newsid\": 2\n}\n",
            "grant_type": 0,
            "holder_data": "",
            "holder_type": 4,
            "index": 17,
            "issuer_data": "",
            "issuer_type": 4,
            "owner": "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP",
            "pid": 70
        },
        ...
  ]
}
```

---

## **GET /api/v2/transaction/\<TXID\>**

Return the transaction `<TXID>`, auto detection of the layer

```js
{
    "data": {
        "amount_pid": 0,
        "amount_xep": 100000000,
        "block": 1916035,
        "block_hash": "a60fe6e87f3e45d30bf1a769effaa17168e66aed41d077ab210ef19caac8d116",
        "body": "",
        "data_content": "",
        "data_type": 4,
        "decimals": true,
        "header": "",
        "invalid_reason": "",
        "l2_fee": 0,
        "layer": "XEP",
        "pid": 0,
        "recipient": {
            "xKutgZdyAPAnHrYE5APQ8NQPBK7DwgWgi6": 100000000
        },
        "sender": [
            "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP"
        ],
        "timestamp": 1762255424,
        "token_end": 0,
        "token_start": 0,
        "trade_pid_1": 0,
        "trade_pid_2": 0,
        "txid": "c5e97b1608787f1c6d525aa077b9a32452dc41f16ee2f8e00955af0b37b5e048",
        "type": 306,
        "type_str": "[TRANSFER]",
        "valid": true,
        "xep_fee": 54000
    },
    "error": null
}
```

---

## **GET /api/v2/block/\<BLOCK\>**

Return the transactions in block `<BLOCK>`

```js
{
    "data": [
        {
            "amount_pid": 0,
            "amount_xep": 32646722309,
            "block": 1934918,
            "block_hash": "11c5a1717217ca0456402ddba55643f46c433fd0caed0adb10001b41abb2dab0",
            "body": "",
            "data_content": "",
            "data_type": 4,
            "decimals": true,
            "header": "",
            "invalid_reason": "",
            "l2_fee": 0,
            "layer": "XEP",
            "pid": 0,
            "recipient": {
                "ep1qm97aarpnepdl6eh934qwm74s2wweer8k42l8x2": 503625925896450
            },
            "sender": [
                "ep1qm97aarpnepdl6eh934qwm74s2wweer8k42l8x2"
            ],
            "timestamp": 1763791104,
            "token_end": 0,
            "token_start": 0,
            "trade_pid_1": 0,
            "trade_pid_2": 0,
            "txid": "f42614e089c2dee57154828915a4bf31807188262242d46a3022cf0dffb4a49a",
            "type": 304,
            "type_str": "[STAKE]",
            "valid": true,
            "xep_fee": 0
        },
        ...
    ],
    "error": null
}
```

---

## **GET /api/v2/omnixep/contracts/updateindex**

Return the basic information/updates of all OmniXEP Contracts. 

```js
{
  "error": null,
  "data": [
        {
            "decimals": true,
            "is_nft": false,
            "name": "Electra Protocol",
            "pid": 0,
            "update_index": 8           // Incremented each time a verified contract has updated its public information (icon, info, ....)
        },
        {
            "decimals": false,
            "is_nft": false,
            "name": "OmniXEP Release party token",
            "pid": 3,
            "update_index": 5
        },
        {
            "decimals": false,
            "is_nft": false,
            "name": "Tekov BEACH volleyball",
            "pid": 4,
            "update_index": 0
        },
        {
            "decimals": false,
            "is_nft": true,
            "name": "OmniXEP Release Party NFT",
            "pid": 5,
            "update_index": 5
        },
        ...
  ]
}
```

---

## **GET /api/v2/omnixep/contracts**

Return the contract(s) detail of provided pid(s)

Query parameters:

| Parameter | Default | Description |
|----------|---------|-------------|
| pid      | NONE      | Contract PID > 2, Support both repeated pid=PID and comma separated |
| page     | 1       | Page number |
| count    | 100     | Items per page |

```js
{
    "data": [
        {
            "cat": "Utility",
            "data": "commemorative token from OmniXEP release party, 29. April 2024",
            "decimals": false,
            "delegate": "",
            "icon_16": "iVBORw0KGgoAAAA.....AAAAABJRU5ErkJggg==",   //base64
            "icon_32": "iVBORw0KGgoAAAA.....AAAABJRU5ErkJggg==",    //base64
            "is_nft": false,
            "issuer": "xJAHuZUkq2A8p89jt4aEiiZUPePS9tdSKW",
            "name": "OmniXEP Release party token",
            "pid": 3,
            "subcat": "AIRDROP",
            "ticker": "ORP",
            "total_holders": "126",
            "total_tokens": "125,000",
            "txid": "eefa3ac57217a60dd73f4d8343a691e51b013c3c4accdafd03a3e5275df723c5",
            "type": 2,
            "type_str": "[Managed Supply]",
            "update_index": 5,
            "url": "https://www.electraprotocol.com/omnixep/",
            "verified": true
        },
        ...
    ],
    "error": null
}
```

---

## **GET /api/v2/omnixep/contracts/\<PID\>**

Same as `/api/v2/omnixep/contracts` without query

---

## **POST /api/v2/omnixep/rawsendtoken**

Request body:
```js
{
    "property_id": 113,     // 0 for XEP transaction
    "sender": "xKutgZdyAPAnHrYE5APQ8NQPBK7DwgWgi6",
    "recipient": "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP",
    "amount": 100000000     // WARNING - amount must be in SATOSHI for XEP and contract having decimals
}
```

Response:
```js
{
  "error": null,
  "data": {
    "inputs": [
        // Utxos selected for the transaction
        {
        "txid": ".....",
        "vout": 1,
        "amount": 100000000 // SATOSHI
        },
        ...
        ],
    "fee": 0.000260,
    "l2_fee": 0.00054,  // 0 for XEP txs
    "raw_tx": "....",  // hex raw transaction to be signed
    "decoded_tx": {
        .... // human readable raw transaction
        },
    "recipient_warning": "NONE"
  }
}
```

---

## **POST /api/v2/omnixep/rawsendnft**

Request body:
```js
{
    "property_id": 88,
    "sender": "xKutgZdyAPAnHrYE5APQ8NQPBK7DwgWgi6",
    "recipient": "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP",
    "token_start": 1,
    "token_end": 1
}
```

---

## **POST /api/v2/omnixep/rawminttoken**

Request body:
```js
{
    "property_id": 114,
    "sender": "xKutgZdyAPAnHrYE5APQ8NQPBK7DwgWgi6",
    "recipient": "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP",
    "amount": 100000000     // WARNING - amount must be in SATOSHI contract having decimals
}
```

---

## **POST /api/v2/omnixep/rawmintnft**

Request body:
```js
{
    "property_id": 88,
    "sender": "xKutgZdyAPAnHrYE5APQ8NQPBK7DwgWgi6",
    "recipient": "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP",
    "amount": 1;
    "data": "", // Data to be added to NFT in 'grant' field on minting
    "data_type": 0 // JSON: 0, URL: 1, IMAGE: 2, RAW TEXT: 4 (TEXT is set by default and if "data" is empty or wrong)
}
```

---

## **POST /api/v2/sendrawtransaction**

Request body:
```js
{
  "raw_tx": "...." // Signed raw transaction
}
```

Response:
```js
{
  "error": null,
  "data": "......" // Transaction ID (hex string)
}
```
---

## **GET /api/v2/utxos**

Query parameters:

| Parameter | Default | Description |
|----------|---------|-------------|
| txid      | NONE      | valid txid 64 chars |
| vout     | NONE       | txid output |

Response:
```js
{
  "error": null,
  "data": {
    "utxo_spent": false,
    // Following keys exist only if the UTXO is not spent
    "bestblock": "327c6ac54d2f21ef0159fce1fecba9b1e783c0bd8a5b29275eb581e133b67e6d",
    "coinbase": false,
    "confirmations": 175062,
    "scriptPubKey": {
        "addresses": [
            "xWzvSGpYUPucJaodadUh3yzEmLJGvHUYsP"
        ],
        "asm": "OP_HASH160 f8f136b5a4c0f66770363a86ec00bbbc640bf7c1 OP_EQUAL",
        "hex": "a914f8f136b5a4c0f66770363a86ec00bbbc640bf7c187",
        "reqSigs": 1,
        "type": "scripthash"
    },
    "value": 0.2 //Here amounts are REAL, no satoshi
  }
}
```

---

## **GET /api/v2/omnixep/nft/\<PID\>/\<ID\>**

Return the NFT data from Contract `PID` and NFT index `ID`

Response:
```js
{
    "data": {
        "grant_data": "https://e7.pngegg.com/pngimages/310/528/png-clipart-futurama-bender-art-futurama-jake-the-dog-bender-professor-farnsworth-cartoon-futurama-heroes-superhero.png",
        "grant_type": 2,    // JSON: 0, URL: 1, IMAGE: 2, RAW TEXT: 4
        "holder_data": "",
        "holder_type": 4,   // JSON: 0, URL: 1, IMAGE: 2, RAW TEXT: 4
        "index": 2,         // NFT id
        "issuer_data": "",
        "issuer_type": 4,   // JSON: 0, URL: 1, IMAGE: 2, RAW TEXT: 4
        "owner": "xBpsK8NKeo1pEqWhizXkhCoU8BZtF976EU",
        "pid": 88
    },
    "error": null
}
```

---

## **GET /api/v2/lasttransactions**

Return the last transactions of the layers, including the mempool transactions waiting to be included in a block

Query parameters:

| Parameter | Default | Description |
|----------|---------|-------------|
| count    | 5       | Allow 1 to 100 |

Response:
```js
{
    "data": [
        {
            "amount_xep": 11315725462,
            "layer": "XEP",
            "timestamp": 1763796720,
            "txid": "309e8e29283c268d9281703c15e3da60e32b3da8fdb8e94fb96d91f4797e06dd"
        },
        {
            "amount_xep": 35095323404,
            "layer": "XEP",
            "timestamp": 1763796480,
            "txid": "c86325783ae8f8c2a17ce9036750a423aa703bac0951e9b77194a93b78899701"
        },
        {
            "amount_xep": 79743608811,
            "layer": "XEP",
            "timestamp": 1763796368,
            "txid": "7d0b488043d6833139054b3220798cab671555784024b4d7ef424601422d803c"
        },
        {
            "amount_xep": 10169779722,
            "layer": "XEP",
            "timestamp": 1763796320,
            "txid": "8e28f1dd599f48e52f6dd390c97ae78c347aec7fa6a8159ec9c634d54df4f98a"
        },
        {
            "amount_xep": 17249400896,
            "layer": "XEP",
            "timestamp": 1763796224,
            "txid": "cfbce941b0f735b9bbf7de1ddbc43c497a17dfdef82532e27a8123d48b2f4c4e"
        }
    ],
    "error": null
}
```

---

## **GET /api/v2/lastblocks**

Query parameters:

| Parameter | Default | Description |
|----------|---------|-------------|
| count    | 5       | Allow 1 to 100 |

Return the last blocks of the blockchain

```js
{
    "data": [
        {
            "hash": "ce455ac204a9d498f7c1a0c6606174f4c252752b3542bcb5663fa1dd3f0d352f",
            "height": 1934987,
            "timestamp": 1763796896
        },
        {
            "hash": "71221947dfb7985b98db7f77c23cc0aaf1e9c5d64dd8cfeeda28c38f810039a5",
            "height": 1934986,
            "timestamp": 1763796880
        },
        {
            "hash": "9156e9da58d6c84e6f979dd9ea45b0dd3c78799afab98256e7574d30d304d715",
            "height": 1934985,
            "timestamp": 1763796720
        },
        {
            "hash": "3094e5febaadcc0e248b1dd5804a13cdc77b66c50be38b0978ab4e9c5c5a0af4",
            "height": 1934984,
            "timestamp": 1763796480
        },
        {
            "hash": "f213139adeb68350de2d101cba609aa44df1fe64b60a46f1f868d1c6fb7e4d0a",
            "height": 1934983,
            "timestamp": 1763796368
        }
    ],
    "error": null
}
```

