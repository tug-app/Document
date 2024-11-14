# MagicEden Sniper Bot 后端接口文档
## Launchpad 看板模块
### NFT Launchpad 列表
#### 路径

**GET** `/v1/launchpad/list`

#### 描述

> 获取 ME BTC 板块 Launchpad 列表，只显示近期的 NFT 项目

#### 请求头

- **token**（必填，字符串）：API 鉴权参数

#### 请求参数

**无**

#### 响应示例
##### 响应成功

```json
{
    "status":"success",
    "message":"ok",
    "data":[
        {
            "name": "The Orange Pills (TOP)",
            "description": "The Orange Pills visually represent the \"orange pilling\" concept—awakening to Bitcoin’s transformative potential and embracing decentralization and true ownership.",
            "url": "/ordinals/launchpad/top",
            "imageURL": "https://media.cdn.magiceden.dev/launchpad/upload/c302a196-a87d-4d4e-8bf3-bd1bc1f29e7c",
            "price": 0.00001,
            "status": "ended",
            "startDate": "2024-11-06T15:00:00.000Z",
            "endDate": "2024-11-12T15:00:00.000Z",
            "mintInfo": {
                "totalSupply": 5555,
                "presaleSupply": 555,
                "broadcasted": 5000
            }
        },
        {
            "name": "Pizza Aliens",
            "description": "Pizza Aliens: 3,333 Bitcoin Ordinal PFPs blending pop culture with blockchain. Aliens are here to conquer and build a bridge between the Web2 world and Web3",
            "url": "/ordinals/launchpad/pizzaaliens",
            "imageURL": "https://img-cdn.magiceden.dev/rs:fill:400:0:0/plain/https://creator-hub-prod.s3.us-east-2.amazonaws.com/ord-pizzaaliens_pfp_1729261557782.png",
            "price": 0.000333,
            "status": "live",
            "startDate": "2024-11-11T15:30:00.000Z",
            "endDate": "2024-11-23T17:30:00.000Z",
            "mintInfo": {
                "totalSupply": 3333,
                "presaleSupply": 50,
                "broadcasted": 807
            }
        },
        {
            "name": "Season 0 : Casey’s Collection",
            "description": "This is the first  ordinal collection made by Inscripedia. The stories were written by Casey Rodarmor.",
            "url": "/ordinals/launchpad/season0",
            "imageURL": "https://media.cdn.magiceden.dev/launchpad/upload/b58e0703-189b-4aa2-aebc-d8c355055625",
            "price": 0.00069,
            "status": "ended",
            "startDate": "2024-11-13T20:00:00.000Z",
            "endDate": "2024-11-21T16:00:00.000Z",
            "mintInfo": {
                "totalSupply": 3000,
                "presaleSupply": 300,
                "broadcasted": 2700
            }
        },
        {
            "name": "Cypher Punks",
            "description": "Cypher Punks is a PFP collection of Bitcoin Ordinals, created to honor the community that helped create Bitcoin on the old forums together with Satoshi Nakamoto. With futuristic Cyber ​​Punk-themed art, the collection is much more than just a PNG, each Cypher Punk is an AaaA (Art as an Application), with javascript and HTML codes behind each inscription, allowing the holder to apply different stickers to their ordinal, change the background or even resize their art to up to 10,000 pixels and download it, all directly onchain within the inscription.",
            "url": "/ordinals/launchpad/cypherpunkss",
            "imageURL": "https://bafybeibe3bxznv5uj7hw2ymiflt7c7avfrireqrzwdfd5gsxwmihaigxpy.ipfs.w3s.link/Yv5otI9gOqhnCgdvmEEcEqqgHlkstbTE2LpajfARRIo.png",
            "price": 0.00001,
            "status": "live",
            "startDate": "2024-11-08T14:00:00.000Z",
            "endDate": "2024-11-18T18:40:00.000Z",
            "mintInfo": {
                "totalSupply": 999,
                "presaleSupply": 296,
                "broadcasted": 608
            }
        }
    ]
}
```

##### 响应失败

```json
{
    "status":"error",
    "message":"xxxxxxxxxx",
    "data":[]
}
```

#### 响应说明

- **status**（必填，字符串）：接口响应状态
- **message**（必填，字符串）：接口响应状态描述
- **data**（必填，字符串）：Launchpad 列表数据
    - **name**（必填，字符串）：项目名称
    - **description**（必填，字符串）：项目描述
    - **url**（必填，字符串）：ME Launchpad 链接
    - **imageURL**（必填，字符串）：项目图片链接
    - **price**（必填，number）：项目 Mint 价格
    - **status**（必填，字符串）：项目状态
    - **startDate**（必填，字符串）：项目开始时间
    - **endDate**（必填，字符串）：项目结束时间
    - **mintInfo**（必填，json）：项目 Mint 详情
        - **totalSupply**（必填，number）：供应量
        - **presaleSupply**（必填，number）：预留数量
        - **broadcasted**（必填，number）：已经 Mint 的数量

## 任务模块
### 新建任务
#### 路径

**GET** `/v1/task/create`

#### 描述

> 创建 Mint 任务

#### 请求头

- **token**（必填，字符串）：API 鉴权参数

#### 请求参数

- **collectionSymbol**（必填，字符串）：NFT 在 ME 的唯一标识，以 NFT 在 ME Launchpad 的 URL 最后一个参数为准。例如 `https://magiceden.io/ordinals/launchpad/season0` 就代表唯一标识是 `season0`
- **address**（必填，字符串）：钱包地址，`bc1p` 或者 `bc1q` 开头的地址。例如：`bc1pxxxxxxxxxxxxxxxxx`
- **publicKey**（必填，字符串）：钱包地址对应的公钥。例如：`02xxxxxxxxxxxx`
- **round**（必填，number）：参与抢购的轮次
- **count**（可选，number）：购买次数，默认是 1 次，如果购买多个，会创建多个任务

#### 响应示例
##### 响应成功

```json
{
    "status":"success",
    "message":"xxxxxxxxxx",
    "data":[
        {
            "taskID": "xxxxxxx",
            "createDate": "2024-11-11T11:00:00.000Z"
        }, 
        {
            "taskID": "xxxxxxx",
            "createDate": "2024-11-11T11:00:00.000Z"
        }
    ]
}
```

##### 响应失败

```json
{
    "status":"error",
    "message":"xxxxxxxxxx",
    "data":[]
}
```

### 任务列表
#### 路径

**GET** `/v1/task/list`

#### 描述

> 获取 ME BTC 板块 Launchpad 列表，只显示近期的 NFT 项目

#### 请求头

**token**（必填，字符串）：API 鉴权参数

#### 请求参数

**address**（必填，字符串）：bc1p/bc1q 钱包地址

#### 响应示例
##### 响应成功

```json
{
    "status":"success",
    "message":"ok",
    "data":[
        {
            "name": "The Orange Pills (TOP)",
            "status": "waiting",
            "createDate": "2024-11-11T11:00:00.000Z",
            "startDate": "2024-11-06T15:00:00.000Z",
            "unsignedPSBT": "",
            "hash": "",
            "mark": ""
        },
        {
            "name": "Pizza Aliens",
            "status": "success",
            "createDate": "2024-11-11T11:00:00.000Z",
            "startDate": "2024-11-11T15:30:00.000Z",
            "unsignedPSBT":"cHNidP8BAPwCAAAAAgupxw+xxxxxxxxxx...",
            "hash": "fe7b4ac85702e6daee2c1e2xxxxxxxxx...",
            "mark": ""
        },
        {
            "name": "Cypher Punks",
            "status": "live",
            "createDate": "2024-11-11T11:00:00.000Z",
            "startDate": "2024-11-11T15:30:00.000Z",
            "unsignedPSBT": "cHNidP8BAPwCAAAAAgupxw+xxxxxxxxxx...",
            "hash": "",
            "mark": ""
        },
        {
            "name": "Season 0 : Casey’s Collection",
            "status": "failed",
            "createDate": "2024-11-11T11:00:00.000Z",
            "startDate": "2024-11-13T20:00:00.000Z",
            "unsignedPSBT": "",
            "hash": "",
            "mark": "失败原因..."
        }
    ]
}
```

##### 响应失败

```json
{
    "status":"error",
    "message":"xxxxxxxxxx",
    "data":[]
}
```

#### 响应说明

- **status**（必填，字符串）：接口响应状态
- **message**（必填，字符串）：接口响应状态描述
- **data**（必填，字符串）：Launchpad 列表数据
    - **name**（必填，字符串）：项目名称
    - **status**（必填，字符串）：任务状态，live 代表运行中；waiting 代表等待开始；success 代表 Mint 成功；failed 代表 Mint 失败
    - **startDate**（必填，字符串）：任务开始时间
    - **unsignedPSBT**（必填，字符串）：从 ME 获取到的 PSBT Base64 字符串
    - **hash**（必填，字符串）：Mint 交易哈希
    - **mark**（必填，字符串）：任务 Mint 失败原因


### 任务 Minting
#### 路径

**POST** `/v1/psbt/minting`

#### 描述

> 前端对 PSBT 签名后回传完成 Mint

#### 请求头

- **token**（必填，字符串）：API 鉴权参数

#### 请求参数

- **taskID**（必填，字符串）：任务 ID
- **signedPSBT**（必填，字符串）：对 PSBT 签名后的 PSBT 字符串

#### 示例请求

```json
{
    "taskID":"xxxxxxx",
    "signedPSBT":"cHNidP8Bxxxxxxxxx"
}
```

#### 响应示例
##### 响应成功

```json
{
    "status": "ok",
    "message": "",
    "data": [
        {
            "name": "Season 0 : Casey’s Collection",
            "txid": "c3ee26c7685284xxxxxxx..."
        }
    ]
}
```

##### 响应失败

```json
{
  "status": "error",
  "message": "失败原因...",
  "data": []
}
```

## 注意事项

- 请确保提供的比特币地址和公钥有效并对应。