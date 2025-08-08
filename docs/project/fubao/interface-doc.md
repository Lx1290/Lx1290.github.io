## 请求域名

- https://ppr.sci99.com/api

### 获取token

- 请求方式：GET
- 请求地址：/login
- 请求参数：

  | 名称     | 类型   | 是否必填 | 描述                             |
  | -------- | ------ | -------- | -------------------------------- |
  | userName | String | Y        | ceshi0426                        |
  | password | String | Y        | 5ddeff755d654f76d192b0b89a392974 |
- 返回示例：

  ```
  {
    "code": 0,
    "msg": "登录成功",
    "info": {
        "userAgreement": true,
        "privacyAgreement": true,
        "isAdmin": false,
        "userName": "ceshi0426",
        "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJub25TdHIiOiIwVmIyelVMYzlHTU9GN1h5IiwidXNlck5hbWUiOiJjZXNoaTA0MjYiLCJ1c2VySWQiOjQzNjgwMDh9.7aiI6gcMjj1bCTrU-Bfirq6I78szz0APmCymOTsd2SI"
        }
    }
  ```

> <span style="color:red;">以下的所有请求，都需将获取到的token放入到请求头Header中</span>

  | 名称     | 类型   | 是否必填 | 描述                             |
  | -------- | ------ | -------- | -------------------------------- |
  | token | String | Y        | 请求返回的token                     |


### 获取产品权限

- 请求方式：GET
- 请求地址：/user/getProductList
- 返回示例：

```

{
    "code": 0,
    "msg": "成功",
    "info": [
        {
            "industryName": "能源",
            "industryId": 6,
            "children": [
                {
                    "productId": 12545,//产品id
                    "hasWeek": 1,//是否有周度模型，1代表有
                    "children": [
                        {
                            "targetNameAll": "中国沥青商品预测目标价",//目标名称
                            "marketAttr": "中国",
                            "unit": "元/吨",
                            "dataId": 137,
                            "targetId": 41,//目标id
                            "productId": 12545,
                            "id": "6_12545_41",
                            "productName": "沥青"
                        }
                    ],
                    "id": "6_12545",
                    "hasFuture": 1,
                    "productName": "沥青",//产品名称
                    "status": 1
                }
            ]
        }
    ]
}

```

### 获取目标信息

- 请求方式：GET
- 请求地址：/index/targetTopInfo
- 请求参数：
  | 名称     | 类型   | 是否必填 | 描述                             |
  | -------- | ------ | -------- | -------------------------------- |
  | targetId | int | Y        | 目标id                     |

- 返回示例：

```
{
    "code": 0,
    "msg": "成功",
    "info": {
        "targetName": "中国沥青商品预测目标价",//目标名称
        "monthAvgAte": 2.47,//月涨跌幅
        "newAvgValue": "3867.57元/吨",//最新价格
        "weekAvgValue": "3849.43元/吨",//周均价
        "lastMonth": "2025-06-01",
        "weekAvgAte": 2.10,//周涨跌幅
        "newAvgAte": 0.48,//日涨跌幅
        "monthAvgValue": "3789.48元/吨",//月均价
        "lastWeek": "2025-06-15",
        "desc": {
            "explain": "取自沥青商品国内主流市场（或企业）的平均价格或代表价格，用以参考国内市场主流价格趋势；取自规格牌号：70#A、90#A；取自市场：东北市场、华东市场、华北市场、华南市场、山东市场、川渝市场、西北市场；运算数据生成时间为日内13：00~18：00，以18:00生成的数据为准。",//数据说明
            "unit": "元/吨",//单位
            "name": "主流市场沥青日度均价（现款现汇）",
            "time": "2013.12-2025.06"//统计周期
        }
    }
}
```

### 预测结果

- 请求方式：GET
- 请求地址：/factorCast/getPprValue
- 请求参数：
  | 名称     | 类型   | 是否必填 | 描述                             |
  | -------- | ------ | -------- | -------------------------------- |
  | targetId | int | Y        | 目标id                     |
  |frequency|str|Y|week:周度，month：月度|
- 返回示例：
```
{
    "code": 0,
    "msg": "成功",
    "info": {
        "startWeek": 26,//开始周数
        "advanceValue": [//领先预测
            {
                "dataMonth": "2025-06-28",
                "value": 3878.46
            },
            {
                "dataMonth": "2025-07-05",
                "value": 3894.27
            },
            {
                "dataMonth": "2025-07-12",
                "value": 3904.35
            },
            {
                "dataMonth": "2025-07-19",
                "value": 3906.83
            }
        ],
        "dataList": [//echarts数据
            {
                "dataMonth": "2015-01-17",//日期
                "ai15": null,//置信区间15%
                "his": 3200.8333,//历史值
                "ai": null,//预测值
                "ai85": null//置信区间85%
            },
            {
                "dataMonth": "2015-01-24",
                "ai15": null,
                "his": 3070.8333,
                "ai": null,
                "ai85": null
            },
            {
                "dataMonth": "2015-01-31",
                "ai15": null,
                "his": 3040.8333,
                "ai": null,
                "ai85": null
            }
        ],
        "startTime": "2025-06-28",//开始周
        "endTime": "2025-07-19",//结束周
        "endWeek": 29,//结束周数
        "items": [//图例
            {
                "targetNameAll": "中国沥青商品预测目标价",
                "unit": "元/吨",
                "marketAttr": "中国",
                "dataId": 137,
                "productId": 12545,
                "dataModel": "",
                "dataName": "中国沥青日度均价(现款现汇)",
                "id": "his",
                "productName": "沥青",
                "lineType": 1,
                "itemName": "真实值"
            },
            {
                "targetNameAll": "中国沥青商品预测目标价",
                "unit": "元/吨",
                "marketAttr": "中国",
                "dataId": 137,
                "productId": 12545,
                "dataModel": "",
                "dataName": "中国沥青日度均价(现款现汇)",
                "id": "ai",
                "productName": "沥青",
                "lineType": 0,
                "itemName": "AI预测"
            },
            {
                "targetNameAll": "中国沥青商品预测目标价",
                "unit": "元/吨",
                "marketAttr": "中国",
                "dataId": 137,
                "productId": 12545,
                "dataModel": "",
                "dataName": "中国沥青日度均价(现款现汇)",
                "id": "ai85",
                "productName": "沥青",
                "lineType": 0,
                "itemName": "置信区间85%线"
            },
            {
                "targetNameAll": "中国沥青商品预测目标价",
                "unit": "元/吨",
                "marketAttr": "中国",
                "dataId": 137,
                "productId": 12545,
                "dataModel": "",
                "dataName": "中国沥青日度均价(现款现汇)",
                "id": "ai15",
                "productName": "沥青",
                "lineType": 0,
                "itemName": "置信区间15%线"
            }
        ],
        "currentValue": [//当期预测
            {
                "dataMonth": "2025-06-28",
                "value": null
            },
            {
                "dataMonth": "2025-07-05",
                "value": null
            },
            {
                "dataMonth": "2025-07-12",
                "value": null
            },
            {
                "dataMonth": "2025-07-19",
                "value": null
            }
        ]
    }
}
```

### 获取模型信息
- 请求方式：GET
- 请求地址：/factorCast/modelInfo
- 请求参数：
  | 名称     | 类型   | 是否必填 | 描述                             |
  | -------- | ------ | -------- | -------------------------------- |
  | targetId | int | Y        | 目标id                     |
  |frequency|str|Y|week:周度，month：月度|

- 返回示例：

```
{
    "code": 0,
    "msg": "成功",
    "info": {
        "agriName": "BVAR模型",//模型算法
        "productId": 12545,
        "targetId": 41,
        "addTime": "2025-03-13 10:54:37",//模型更新时间
        "forecastLength": 3,
        "sampleCnt": 30000,
        "modelType": 1,
        "frequency": "month",
        "isShow": 1,
        "modelName": "月度预测模型",//模型方案
        "unit": "元/吨",
        "modelCode": "scibase_bvar",
        "hisCycle": "2017-05-12 00:00:00",
        "id": 6002,//模型id
        "pprTime": "2025-06-09 02:04:36",//预测更新时间
        "featureMode": "月度均值",
        "factorEnd": "2025-05",//历史估计周期-结束
        "factorStart": "2017-05",//历史估计周期-开始
        "predictMonth": "2025-06-01",
        "nextUpdateTime": "2025-06-24 18:00:00",
        "round": 2,
        "modelCycle": "月度模型"
    }
}
```

### 因子贡献度
- 请求方式：GET
- 请求地址：/factorCast/divisorContriByCycle
- 请求参数：
  | 名称     | 类型   | 是否必填 | 描述                             |
  | -------- | ------ | -------- | -------------------------------- |
  | targetId | int | Y        | 目标id                     |
  |frequency|str|Y|week:周度，month：月度|
  |modelId|int|Y|模型id|

- 返回示例：

```
{
    "code": 0,
    "msg": "成功",
    "info": {
        "dataList": [
            {
                "dataMonth": "2025-04",//日期
                "24690": -0.0142532,//对应items里的id
                "24681": 0.0489179,
                "24680": -0.0112619,
                "24682": 0.0740722,
                "24685": 0.0123404,
                "24684": 0.038906,
                "24676": 0.543088,
                "24689": 0.079791,
                "24677": 0.170132,
                "24688": 0.00723801
            },
            {
                "dataMonth": "2025-05",
                "24690": -0.0881006,
                "24681": 0.0394153,
                "24680": 0.0260237,
                "24682": 0.0765081,
                "24685": 0.00732388,
                "24684": 0.0352818,
                "24676": 0.428046,
                "24689": 0.0898969,
                "24677": 0.114683,
                "24688": -0.0947204
            },
            {
                "dataMonth": "2025-06",
                "24690": -0.0139223,
                "24681": 0.0375487,
                "24680": 0.031463,
                "24682": 0.0770495,
                "24685": 0.0104313,
                "24684": 0.0241591,
                "24676": 0.436422,
                "24689": 0.0639486,
                "24677": 0.163221,
                "24688": -0.141834
            }
        ],
        "startTime": "2025-04",//开始时间
        "endTime": "2025-06",//结束时间
        "items": [//因子列表
            {
                "isTarget": 1,
                "isStandard": 1,
                "dataId": 137,
                "divisorName": "中国沥青日度均价(现款现汇)",
                "addTime": "2025-03-13 10:54:37",
                "modelId": 6002,
                "isOut": 0,
                "id": 24676,
                "dsDivisorId": 15443,
                "startDate": "2013-12-04 00:00:00",
                "isIn": 1,
                "isMix": 1
            },
            {
                "isTarget": 0,
                "isStandard": 1,
                "dataId": 1430,
                "divisorName": "华东沥青周度库容率",
                "addTime": "2025-03-13 10:54:37",
                "modelId": 6002,
                "isOut": 0,
                "id": 24677,
                "dsDivisorId": 15452,
                "startDate": "2015-01-01 00:00:00",
                "isIn": 1,
                "isMix": 1
            },
            {
                "isTarget": 0,
                "isStandard": 1,
                "dataId": 1426,
                "divisorName": "中国沥青月度企业库存",
                "addTime": "2025-03-13 10:54:37",
                "modelId": 6002,
                "isOut": 0,
                "id": 24680,
                "dsDivisorId": 15461,
                "startDate": "2011-01-31 00:00:00",
                "isIn": 1,
                "isMix": 0
            },
            {
                "isTarget": 0,
                "isStandard": 1,
                "dataId": 1434,
                "divisorName": "中国沥青月度进口量",
                "addTime": "2025-03-13 10:54:37",
                "modelId": 6002,
                "isOut": 0,
                "id": 24681,
                "dsDivisorId": 15464,
                "startDate": "2005-02-28 00:00:00",
                "isIn": 1,
                "isMix": 0
            },
            {
                "isTarget": 0,
                "isStandard": 1,
                "dataId": 583,
                "divisorName": "房地产竣工面积_累计值",
                "addTime": "2025-03-13 10:54:37",
                "modelId": 6002,
                "isOut": 0,
                "id": 24682,
                "dsDivisorId": 15467,
                "startDate": "2013-08-31 00:00:00",
                "isIn": 1,
                "isMix": 0
            },
            {
                "isTarget": 0,
                "isStandard": 1,
                "dataId": 1452,
                "divisorName": "山东省沥青周度毛利",
                "addTime": "2025-03-13 10:54:37",
                "modelId": 6002,
                "isOut": 0,
                "id": 24684,
                "dsDivisorId": 15473,
                "startDate": "2015-01-01 00:00:00",
                "isIn": 1,
                "isMix": 1
            },
            {
                "isTarget": 0,
                "isStandard": 1,
                "dataId": 1458,
                "divisorName": "中国原油炼油综合生产日度税后装置毛利",
                "addTime": "2025-03-13 10:54:37",
                "modelId": 6002,
                "isOut": 0,
                "id": 24685,
                "dsDivisorId": 15476,
                "startDate": "2017-05-12 00:00:00",
                "isIn": 1,
                "isMix": 1
            },
            {
                "isTarget": 0,
                "isStandard": 1,
                "dataId": 337,
                "divisorName": "伦敦洲际交易所(ICE)原油(布伦特)日度期货结算价",
                "addTime": "2025-03-13 10:54:37",
                "modelId": 6002,
                "isOut": 1,
                "id": 24688,
                "dsDivisorId": 17048,
                "startDate": "2000-12-01 00:00:00",
                "isIn": 1,
                "isMix": 1
            },
            {
                "isTarget": 0,
                "isStandard": 1,
                "dataId": 1462,
                "divisorName": "山东市场渣油(低硫渣油)日度市场价(现款现汇)",
                "addTime": "2025-03-13 10:54:37",
                "modelId": 6002,
                "isOut": 0,
                "id": 24689,
                "dsDivisorId": 17051,
                "startDate": "2005-04-19 00:00:00",
                "isIn": 1,
                "isMix": 1
            },
            {
                "isTarget": 0,
                "isStandard": 1,
                "dataId": 17186,
                "divisorName": "期现基差",
                "addTime": "2025-03-13 10:54:37",
                "modelId": 6002,
                "isOut": 0,
                "id": 24690,
                "dsDivisorId": 18718,
                "startDate": "2013-12-04 00:00:00",
                "isIn": 1,
                "isMix": 1
            }
        ]
    }
}
```


### 因素列表

- 请求方式：GET
- 请求地址：factor/map
- 请求参数：
  | 名称     | 类型   | 是否必填 | 描述                             |
  | -------- | ------ | -------- | -------------------------------- |
  |targetId | int | Y        | 目标id                     |

- 返回示例：

```
{
    "code": 0,
    "msg": "成功",
    "info": {
        "targetNameAll": "中国沥青商品预测目标价",
        "unit": "元/吨",
        "marketAttr": "中国",
        "dataId": 137,
        "productId": 12545,
        "dataModel": "",
        "dataName": "中国沥青日度均价(现款现汇)",
        "id": 41,
        "productName": "沥青",
        "items": [
            [
                {
                    "productId": 12545,
                    "targetId": 41,
                    "location": "上1",//展示位置
                    "id": 394,
                    "firstNodeName": "成本",//节点名称
                    "items": [
                        {
                            "secondNodeName": "国际油价",//二级节点名称
                            "sortId": 1,
                            "firstNodeId": 394,
                            "id": 966,
                            "items": [
                                {
                                    "secondNodeId": 966,
                                    "isRecommend": 1,
                                    "productId": 12545,
                                    "targetId": 41,
                                    "influenceInstructions": "原油是沥青的直接原料，原料定价参考布伦特，成本跟布伦特成正相关性。",
                                    "lag": "不滞后",
                                    "originId": "9195_354",
                                    "dataId": 337,
                                    "influenceCycle": "长期影响（持续时间3个月至一年）",
                                    "sortId": 17,
                                    "factorName": "伦敦洲际交易所(ICE)原油（布伦特）日度主力合约期货结算价",//因素名称
                                    "id": 1620,
                                    "direction": "正相关",
                                    "type": 0,
                                    "time": "2025-08-01",//最新日期
                                    "isValid": true,
                                    "value2": "-3.94",//涨跌幅
                                    "value1": "69.67",//最新值
                                    "dataTypePathID": "23085",
                                    "dataTypePath3": "结算价（Settlement Price）是当天交易结束后，对未平仓合约进行当日交易保证金及当日盈亏结算的基准价。",
                                    "dataTypePath2": "是指期货市场上通过公开竞价方式形成的期货合约标的物的价格。",
                                    "unit": "美元/桶"//单位
                                }
                            ]
                        }
                    ]
                },
                {
                    "productId": 12545,
                    "targetId": 41,
                    "location": "上2",
                    "id": 403,
                    "firstNodeName": "利润",
                    "items": [
                        {
                            "secondNodeName": "沥青生产利润",
                            "sortId": 1,
                            "firstNodeId": 403,
                            "id": 944,
                            "items": [
                                {
                                    "secondNodeId": 944,
                                    "isRecommend": 1,
                                    "productId": 12545,
                                    "targetId": 41,
                                    "influenceInstructions": "利润增加，会刺激沥青产量增加，供应增大，利空价格。",
                                    "lag": "不滞后",
                                    "originId": "68859_194",
                                    "dataId": 1452,
                                    "influenceCycle": "中期影响（持续时间1-3个月）",
                                    "sortId": 18,
                                    "factorName": "山东省沥青周度毛利",
                                    "id": 1622,
                                    "direction": "负相关",
                                    "type": 0,
                                    "time": "2025-07-31",
                                    "isValid": true,
                                    "value2": "8.43",
                                    "value1": "-397.50",
                                    "dataTypePathID": "23086",
                                    "dataTypePath3": "商业企业商品销售收入（售价）减去商品原进价后的余额",
                                    "dataTypePath2": "反映成本利润的一系列指标",
                                    "unit": "元/吨"
                                },
                                {
                                    "secondNodeId": 944,
                                    "isRecommend": 0,
                                    "productId": 12545,
                                    "targetId": 41,
                                    "influenceInstructions": "利润增加，会刺激沥青产量增加，供应增大，利空价格。",
                                    "lag": "不滞后",
                                    "originId": "131135_194",
                                    "dataId": 1454,
                                    "influenceCycle": "中期影响（持续时间1-3个月）",
                                    "sortId": 19,
                                    "factorName": "江苏省沥青周度毛利",
                                    "id": 1624,
                                    "direction": "负相关",
                                    "type": 0,
                                    "time": "2025-07-31",
                                    "isValid": true,
                                    "value2": "-6.53",
                                    "value1": "415.20",
                                    "dataTypePathID": "23086",
                                    "dataTypePath3": "商业企业商品销售收入（售价）减去商品原进价后的余额",
                                    "dataTypePath2": "反映成本利润的一系列指标",
                                    "unit": "元/吨"
                                },
                                {
                                    "secondNodeId": 944,
                                    "isRecommend": 0,
                                    "productId": 12545,
                                    "targetId": 41,
                                    "influenceInstructions": "利润增加，会刺激沥青产量增加，供应增大，利空价格。",
                                    "lag": "不滞后",
                                    "originId": "131140_194",
                                    "dataId": 1456,
                                    "influenceCycle": "中期影响（持续时间1-3个月）",
                                    "sortId": 20,
                                    "factorName": "河北省沥青周度毛利",
                                    "id": 1626,
                                    "direction": "负相关",
                                    "type": 0,
                                    "time": "2025-07-31",
                                    "isValid": true,
                                    "value2": "7.79",
                                    "value1": "-474.39",
                                    "dataTypePathID": "23086",
                                    "dataTypePath3": "商业企业商品销售收入（售价）减去商品原进价后的余额",
                                    "dataTypePath2": "反映成本利润的一系列指标",
                                    "unit": "元/吨"
                                }
                            ]
                        },
                        {
                            "secondNodeName": "汽柴油生产利润",
                            "sortId": 1,
                            "firstNodeId": 403,
                            "id": 953,
                            "items": [
                                {
                                    "secondNodeId": 953,
                                    "isRecommend": 1,
                                    "productId": 12545,
                                    "targetId": 41,
                                    "influenceInstructions": "汽柴油跟沥青利润的对比，汽柴油利润高会降低沥青产量，利好价格；汽柴油利润低会带动沥青产量增加，利空价格。",
                                    "lag": "不滞后",
                                    "originId": "102270_194",
                                    "dataId": 1458,
                                    "influenceCycle": "中期影响（持续时间1-3个月）",
                                    "sortId": 21,
                                    "factorName": "中国原油炼油综合生产日度税后毛利",
                                    "id": 1628,
                                    "direction": "负相关",
                                    "type": 0,
                                    "time": "2025-08-04",
                                    "isValid": true,
                                    "value2": "-3.28",
                                    "value1": "169.46",
                                    "dataTypePathID": "23086",
                                    "dataTypePath3": "商业企业商品销售收入（售价）减去商品原进价后的余额",
                                    "dataTypePath2": "反映成本利润的一系列指标",
                                    "unit": "元/吨"
                                }
                            ]
                        }
                    ]
                }
            ]
        ],
        "centerInfo": {
            "lastMonthChange": 0.0900,
            "latestPrice": "3856.86元/吨",
            "latestChange": -0.1300,
            "unit": "元/吨",
            "name": "沥青商品预测目标价",
            "monthAveragePrice": "3859.36元/吨",
            "latestTime": "2025-08-04",
            "lastMonthAveragePrice": "3855.74元/吨"
        }
    }
}
```

### 单个因素详情

- 请求方式：GET
- 请求地址：/factor/detail
- 请求参数：
  | 名称     | 类型   | 是否必填 | 描述                             |
  | -------- | ------ | -------- | -------------------------------- |
  |factorId | int | Y        | 因素id                     |

- 返回示例：

```
{
    "code": 0,
    "msg": "成功",
    "info": {
        "explain": "是指某一统计时间内产量与产能的比值，是指实际开工负荷率，在企业生产实践中与计划开工负荷率相对应。开工负荷率=产量/产能*100%",//因素说明
        "overview": "<p>日度开工负荷率:34.75%，环比：<span style=\"color:#11bf99\">-3.82%</span>。</p><p>近3个月下跌<span style=\"color:#11bf99\">-3.77%</span>，近6个月上涨<span style=\"color:#fd6864\">18.32%</span>，近12个月上涨<span style=\"color:#fd6864\">10.42%</span>。</p>",//因素概述
        "item": {
            "name": {
                "targatFactorName": "中国沥青商品预测目标价",
                "currentFactorName": "中国沥青日度开工负荷率"
            },
            "value": [
                {
                    "date": "2015-01-01",
                    "targatFactorValue": null,
                    "currentFactorValue": 48.53
                },
                {
                    "date": "2015-01-02",
                    "targatFactorValue": null,
                    "currentFactorValue": 48.53
                },
                {
                    "date": "2015-01-03",
                    "targatFactorValue": null,
                    "currentFactorValue": 48.53
                }
            ]
        },
        "time": "2025-06-18",//更新时间
        "mechanism": "短期影响（1月内消退），不滞后，开工率上涨会有供应增加的预期，利空市场。"//影响机制
    }
}
```


### 预测简报-预测结果
- 请求方式：GET
- 请求地址：/monthReport/getForecastResult
- 请求参数：
  | 名称     | 类型   | 是否必填 | 描述                             |
  | -------- | ------ | -------- | -------------------------------- |
  |targetId | int | Y        | 目标id                     |
  |predictCycle|str|Y|预测期，如：2025-06-01|
  |cycle|int|展示几期，如：3|

- 返回示例：

```
{
    "code": 0,
    "msg": "成功",
    "info": {
        "dataList": [
            {
                "dataCycle": "2025-03",
                "his": 3789.3743,//历史
                "ai": null,//ai预测
                "sci": null//sci预测
            },
            {
                "dataCycle": "2025-04",
                "his": 3686.1104,
                "ai": null,
                "sci": null
            },
            {
                "dataCycle": "2025-05",
                "his": 3698.0977,
                "ai": 3698.0977,
                "sci": 3698.0977
            },
            {
                "dataCycle": "2025-06",
                "his": null,
                "ai": 3695.8,
                "sci": 3673.61
            },
            {
                "dataCycle": "2025-07",
                "his": null,
                "ai": 3631.58,
                "sci": 3663.79
            },
            {
                "dataCycle": "2025-08",
                "his": null,
                "ai": 3572.82,
                "sci": 3585.41
            }
        ],
        "startTime": "2025-06-01",//预测时间
        "endTime": "2025-08",//结束时间
        "items": [//图例
            {
                "targetNameAll": "中国沥青商品预测目标价",
                "unit": "元/吨",
                "marketAttr": "中国",
                "dataId": 137,
                "productId": 12545,
                "dataModel": "",
                "dataName": "中国沥青日度均价(现款现汇)",
                "id": "his",
                "productName": "沥青",
                "lineType": 1,
                "itemName": "真实值"
            },
            {
                "targetNameAll": "中国沥青商品预测目标价",
                "unit": "元/吨",
                "marketAttr": "中国",
                "dataId": 137,
                "productId": 12545,
                "dataModel": "",
                "dataName": "中国沥青日度均价(现款现汇)",
                "id": "ai",
                "productName": "沥青",
                "lineType": 0,
                "itemName": "AI预测"
            },
            {
                "targetNameAll": "中国沥青商品预测目标价",
                "unit": "元/吨",
                "marketAttr": "中国",
                "dataId": 137,
                "productId": 12545,
                "dataModel": "",
                "dataName": "中国沥青日度均价(现款现汇)",
                "id": "sci",
                "productName": "沥青",
                "lineType": 0,
                "itemName": "SCI情景预测"
            }
        ]
    }
}
```

### 预测简报-行情综述
- 请求方式：GET
- 请求地址：/monthReport/getMonthAdvanceComment
- 请求参数：
  | 名称     | 类型   | 是否必填 | 描述                             |
  | -------- | ------ | -------- | -------------------------------- |
  |targetId | int | Y        | 目标id                     |
  |predictCycle|str|Y|预测期，如：2025-06-01|

- 返回示例：

```
{
    "code": 0,
    "msg": "成功",
    "info": {
        "eid": 2603,
        "targetId": 41,
        "addTime": "2025-06-09 13:34:46",
        "month": "2025-06-01 00:00:00",
        "round": 2,
        "modelCode": "scibase_bvar",
        "id": 12597,
        "predictDes": "<p>5月全国沥青市场均价为3698.1元/吨，较上月均价上涨11.99元/吨或0.33%。5月原油月均价环比下跌，成本支撑趋弱，但5月沥青需求稳中改善，炼厂库存暂未累库，供需表现相对稳定，加之沥青期货震荡走高，对本月沥青现货价格存在利好支撑。</p>",//行情综述
        "status": 1
    }
}
```