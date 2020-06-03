## > 基本函数

### >> SAMTrader

### >>> init()

描述：策略入口类构造方法

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  initial | func | 自定义函数 | 实现初始化策略引擎 |
|  on_data | func | 自定以函数 |  实现策略逻辑  |

### >>> initial()

描述：自定义函数，创建策略引擎，并将其返回

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| SAMTraderEngine | 策略引擎对象|

### >>> on_data()

描述： 自定义函数，实现策略逻辑

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  bar | dict | 回测数据 |  一个<string, list>的key-value对象，其中每一项的key是品种名，value是一个KlineData(K线数据) / DepthData(盘口数据) / TickData（Tick数据）的list数组 |
|  e | SAMTraderEngine | 策略引擎对象 |    |

### >>> start()

描述： 策略回测开始

### >> SAMTraderEngine

### >>> init()

描述：策略引擎类构造方法

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  userid | string | 用户Id |  |
|  strategyid | string | 策略Id |    |
|  symbol_list | string | 回测品种 | 支持多品种，多个品种用英文半角逗号(",")隔开   |
|  time_type | string | 时间精度 |  1m（1分钟）、5m（5分钟）、15m（15分钟）、30m（30分钟）、1h（1小时）  |
|  data_type | string | 数据类型 |  kline(k线)、depth(盘口) 、tick（tick）  |
|  get_data_way | string | 获取数据方式 |  1（本地csv）、2（api）、3（同步数据库）、4（自定义数据源）  |
|  data_source_type | string | 市场类型 |  Forex（外汇）、DigitalCurrency（数字货币）  |
|  api_key | string | 访问api的key |  当获取数据方式为2，即通过api获取数据时，需要传入该值  |
|  api_secret | string | 访问api的secret |  当获取数据方式为2，即通过api获取数据时，需要传入该值  |
|  cash | float | 初始资金 |   |
|  starttime | string | 回测开始时间 |  格式：'%Y-%m-%d %H:%M:%S' 或者  '%Y-%m-%d'  |
|  endtime | string | 回测结束时间 | 同上   |
|  fill_bar_type | string | 成交方式类型 |  1：当前bar价格，2：下一bar的价格 ，目前暂时不处理该字段，请传入空字符''  |
|  running_type | string | 数据源类型 |  0： 手动模式，返回数据文件路径；1：自动模式，自动拉取行情数据 , 目前只支持自动模式  |
|  account_type | string | 结算币种 |  账户类型 USD：美元,CNY:人民币，保留  |
|  open_percent | string | 开仓资金占用比例 |  用于开仓的资金所占的比例，默认值为1  |
|  leverage_multiple | string | 杠杆倍数 | 默认为1倍杠杆   |

## > 交易函数

### >> place_order()

描述：下单函数，根据指定的成交价进行下单

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  symbol | string | 交易品种 |  格式如：BTC/USDT.BN （基础币种/计价币种.交易所简称） |
|  direction | string | 交易方向 |  Buy(买)、Sell(卖)  |
|  order_time | string | 下单时间 |  Buy()  |
|  quantity | float | 交易手数或下单量 |    |
|  open_or_close | string | 开仓/平仓 |  Open（开仓）、Close（平仓）  |
|  order_type | int | 订单类型 | 0:市价单，1：限价单  |
|  fillprice | float | 订单成交价 |    |
|  limitprice | float | 订单限价 |  order_type填0此处可不填  |

### >> place_order_percent_capital()

描述：下单函数，按本金指定比例决定开仓量

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  symbol | string | 交易品种 |  格式如：BTC/USDT.BN （基础币种/计价币种.交易所简称） |
|  direction | string | 交易方向 |  Buy(买)、Sell(卖)  |
|  order_time | string | 下单时间 |  Buy()  |
|  open_or_close | string | 开仓/平仓 |  Open（开仓）、Close（平仓）  |
|  order_type | int | 订单类型 | 0:市价单，1：限价单  |
|  fillprice | float | 订单成交价 |    |
|  limitprice | float | 订单限价 |  order_type填0此处可不填  |


备注： 

1、该方法会根据open_ratio(开仓比率)、leverage_multiple（杠杆倍数）决定交易数量,比如capital（本金）为100000，open_ratio为0.1，leverage_multiple为5，则open_cash（开仓使用资金）=capital * open_ratio * leverage_multiple = 50000，

相应的开仓数量为amount = open_cash / fillprice= 50000/ 10000 = 5；

2、在调用该方法进行下单前，开仓比率、杠杆倍数需要在策略引擎初始化时进行相应设置

### >> place_order_percent_cash()

描述：下单函数，按本金指定比例决定开仓量

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  symbol | string | 交易品种 |  格式如：BTC/USDT.BN （基础币种/计价币种.交易所简称） |
|  direction | string | 交易方向 |  Buy(买)、Sell(卖)  |
|  order_time | string | 下单时间 |  Buy()  |
|  open_or_close | string | 开仓/平仓 |  Open（开仓）、Close（平仓）  |
|  order_type | int | 订单类型 | 0:市价单，1：限价单  |
|  fillprice | float | 订单成交价 |    |
|  limitprice | float | 订单限价 |  order_type填0此处可不填  |

备注：

1、该方法会根据open_ratio(开仓比率)、leverage_multiple（杠杆倍数）决定交易数量,比如cash（可用资金）为100000，open_ratio为0.1，leverage_multiple为5，则open_cash（开仓使用资金）=cash * open_ratio * leverage_multiple = 50000，

相应的开仓数量为amount = open_cash / fillprice= 50000/ 10000 = 5；

2、在调用该方法进行下单前，开仓比率、杠杆倍数需要在策略引擎初始化时进行相应设置，具体设置请参考 2.1 构造函数。

### >> get_orders()

描述：获取当前回测的所有订单

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
|list |  list中的每个元素为 StrategyOrder 对象 |

### >> get_account()

描述：获取当前账户的可用资金

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
|float | 当前账户可用资金 |

### >> get_holdings()

描述：获取持仓信息

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
|dict | <string, dict<string, Holding>>的dict对象，其中每一项的key是品种名，value为dict类型(其中， key为持仓方向:Buy/Sell, value为Holding(持仓量)) |


## > 数据查询函数

### >> get_local_csvpath()

描述：返回同步数据的文件路径

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| string | 同步数据的文件路径 |

### >> get_spot_kline_data()

描述：从数据同步后的本地csv路径获取指定时间范围的现货K线数据

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  exchange | string | 交易所 |  |
|  base_symbol | string | 基础币种 |  |
|  asset_symbol | string | 计价币种 |  |
|  period | string | 时间精度 | 1m（1分钟）、5m（5分钟）、15m（15分钟）、30m（30分钟）、1h（1小时）   |
|  start_time | string | 开始时间 |  时间格式：'%Y-%m-%d %H:%M:%S' ，（必填） |
|  end_time | string | 结束时间 |  同上 （必填） |

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为KlineData对象 |

### >> get_future_kline_data()

描述：从数据同步后的本地csv路径获取指定时间范围的期货K线数据

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  exchange | string | 交易所 |  |
|  base_symbol | string | 基础币种 |  |
|  asset_symbol | string | 计价币种 |  |
|  period | string | 时间精度 | 1m（1分钟）、5m（5分钟）、15m（15分钟）、30m（30分钟）、1h（1小时）   |
|  future_type | string | 合约类型 | Q（季度）、TW（当周）、NW（次周） |
|  start_time | string | 开始时间 |  时间格式：'%Y-%m-%d %H:%M:%S' ，（必填） |
|  end_time | string | 结束时间 |  同上 （必填） |

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为KlineData对象 |


### >> get_spot_depth_data()

描述：从数据同步后的本地csv路径获取指定时间范围的现货盘口数据

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  exchange | string | 交易所 |  |
|  base_symbol | string | 基础币种 |  |
|  asset_symbol | string | 计价币种 |  |
|  start_time | string | 开始时间 |  时间格式：'%Y-%m-%d %H:%M:%S' ，（必填） |
|  end_time | string | 结束时间 |  同上 （必填） |

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为DepthData对象 |

### >> get_future_depth_data()

描述：从数据同步后的本地csv路径获取指定时间范围的期货盘口数据

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  exchange | string | 交易所 |  |
|  base_symbol | string | 基础币种 |  |
|  asset_symbol | string | 计价币种 |  |
|  future_type | string | 合约类型 | Q（季度）、TW（当周）、NW（次周） |
|  start_time | string | 开始时间 |  时间格式：'%Y-%m-%d %H:%M:%S' ，（必填） |
|  end_time | string | 结束时间 |  同上 （必填） |

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为DepthData对象 |


### >> get_history_kline_data_by_api()

描述：通过api获取k线历史数据

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  api_key | string | Api_Key |   |
|  api_secret | string | Api_Secrect |    |
|  symbol | string | 交易品种名 |  格式为：基础币种/计价币种.交易对简称，如：BTC/USDT.BN   |
|  period | string | 时间精度 | 1m（1分钟）、5m（5分钟）、15m（15分钟）、30m（30分钟）、1h（1小时）   |
|  start_time | string | 开始时间 |  时间格式：'%Y-%m-%d %H:%M:%S'  |
|  end_time | string | 结束时间 |  同上  |

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为KlineData对象 |


备注：

1、如果starttime和endtime参数同时为空，则返回最近的200条k线数据;starttime和endtime参数要么同时为空，要么同时不为空。

### >> get_sync_spot_kline_data()

描述：通过提供postgresql同步数据库的账号信息以及相关参数获取指定时间范围的现货K线数据

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  exchange | string | 交易所 |   |
|  base_symbol | string | 基础币种 |    |
|  asset_symbol | string | 计价币种 |    |
|  period | string | 时间精度 |  1m（1分钟）、5m（5分钟）、15m（15分钟）、30m（30分钟）、1h（1小时）  |
|  starttime | string | 开始时间 |  时间格式如：'2019-09-09 10:00:00'  |
|  endtime | string | 结束时间 |   同上 |


#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为KlineData对象 |


备注：

1、starttime和endtime都不能为空

### >> get_sync_future_kline_data()

描述：通过提供postgresql同步数据库的账号信息以及相关参数获取指定时间范围的期货K线数据

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  exchange | string | 交易所 |   |
|  base_symbol | string | 基础币种 |    |
|  asset_symbol | string | 计价币种 |    |
|  period | string | 时间精度 |  1m（1分钟）、5m（5分钟）、15m（15分钟）、30m（30分钟）、1h（1小时）  |
|  starttime | string | 开始时间 |  时间格式如：'2019-09-09 10:00:00'  |
|  endtime | string | 结束时间 |   同上 |


#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为KlineData对象 |

备注：

1、starttime和endtime都不能为空

### >> get_sync_forex_kline_data()

描述：通过提供postgresql同步数据库的账号信息以及相关参数获取指定时间范围的外汇K线数据

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  base_symbol | string | 基础币种 |    |
|  asset_symbol | string | 计价币种 |    |
|  period | string | 时间精度 |  1m（1分钟）、5m（5分钟）、15m（15分钟）、30m（30分钟）、1h（1小时）  |
|  starttime | string | 开始时间 |  时间格式如：'2019-09-09 10:00:00'  |
|  endtime | string | 结束时间 |   同上 |


#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为KlineData对象 |

备注：

1、starttime和endtime都不能为空

### >> get_sync_forex_tick_data()

描述：通过提供postgresql同步数据库的账号信息以及相关参数获取指定时间范围的外汇Tick数据

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  base_symbol | string | 基础币种 |    |
|  asset_symbol | string | 计价币种 |    |
|  starttime | string | 开始时间 |  时间格式如：'2019-09-09 10:00:00'  |
|  endtime | string | 结束时间 |   同上 |


#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为TickData对象 |

备注：

1、starttime和endtime都不能为空

## > 交易对信息查询函数

### >> get_spot_symbol_by_api()

描述： 通过提供Api Key、Api Secret以及相关参数获取现货交易对信息

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  api_key | string | Api_Key |   |
|  api_secret | string | Api_Secrect |    |
|  symbol | string | 交易品种名 |  格式为：基础币种/计价币种.交易对简称，如：BTC/USDT.BN   |
|  exchange | string | 交易所 | BN（币安）、OK（Okex）、HB(火币)、BF（Bitfinex）   |

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为SymbolModel对象 |

### >> get_future_symbol_by_api()

描述： 通过提供Api Key、Api Secret以及相关参数获取期货交易对信息

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  api_key | string | Api_Key |   |
|  api_secret | string | Api_Secrect |    |
|  symbol | string | 交易品种名 |  格式为：基础币种/计价币种.交易对简称，如：BTC/USDT.BN   |
|  exchange | string | 交易所 | BN（币安）、OK（Okex）、HB(火币)、BF（Bitfinex）   |

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为FuturesModel对象 |

### >> get_index_symbol_by_api()

描述： 通过提供Api Key、Api Secret以及相关参数获取指数交易对信息

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  api_key | string | Api_Key |   |
|  api_secret | string | Api_Secrect |    |
|  symbol | string | 交易品种名 |  格式为：基础币种/计价币种.交易对简称，如：BTC/USDT.BN   |
|  exchange | string | 交易所 | BN（币安）、OK（Okex）、HB(火币)、BF（Bitfinex）   |

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为IndexModel对象 |

### >> get_option_symbol_by_api()

描述： 通过提供Api Key、Api Secret以及相关参数获取期权交易对信息

#### Parameters
| 参数名称 |  类型  |  参数描述  |  备注  |
|  :---  |  :---  |  :--- | :---  |
|  api_key | string | Api_Key |   |
|  api_secret | string | Api_Secrect |    |
|  symbol | string | 交易品种名 |  格式为：基础币种/计价币种.交易对简称，如：BTC/USDT.BN   |
|  exchange | string | 交易所 | BN（币安）、OK（Okex）、HB(火币)、BF（Bitfinex）   |

#### Return
|  类型  |  备注  |
|  :---  |  :---  |
| list | 每一项为IndexModel对象 |


## > 数据结构

### >> KlineData -- k线数据

#### Atrribute
| 属性 |  类型  |  描述  |
|  :---  |  :---  |  :--- |
| symbol    | string   | 品种   |
| bar_time    | string   | 报价时间   |
| high    | float   | 最高价   |
| low    | float   | 最低价   |
| open    | float   | 开盘价   |
| close    | float   | 收盘价   |
| quote_volume    | float   | 基础币种成交量   |
| quoteasset_volume    | float   | 计价币种成交量（okex期货合约表示合约张数，单位为张）   |
| trade_num    | float   | 交易笔数   |

### >> DepthData -- 盘口数据

#### Atrribute
| 属性 |  类型  |  描述  |
|  :---  |  :---  |  :--- |
| symbol    | string   | 品种   |
| bar_time    | string   | 报价时间   |
| bids_price_list    | list（float）   | 买20价 |
| bids_quantity_list    | list（float）   | 买20量   |
| asks_price_list    | list（float）   | 卖20价   |
| asks_quantity_list    | list（float）  | 卖20量   |

### >> TickData -- Tick数据

#### Atrribute
| 属性 |  类型  |  描述  |
|  :---  |  :---  |  :--- |
| symbol    | string   | 品种   |
| bar_time    | string   | 报价时间   |
| bid    | float   | 买价 |
| ask    | float  | 卖价   |

### >> SymbolModel -- 现货交易对

#### Atrribute
| 属性 |  类型  |  描述  |
|  :---  |  :---  |  :--- |
| symbol    | string   | matrixdata统一交易对   |
| baseasset    | string   | 基础币种   |
| quoteasset    | string   | 计价币种   |
| type    | SymbolTypeModel   | 交易对类型，具体属性参考 SymbolTypeModel类属性说明  |
| status    | string   | 状态   |
| displaysymbol    | string   | 交易所显示交易对   |
| tradesymbol    | string   | 交易所接口交易对   |
| exchange    | string   | 交易所   |
| listedtime    | string   | 上市时间   |
| delistedtime    | string   | 退市时间   |

### >> SymbolTypeModel -- 交易对类型

#### Atrribute
| 属性 |  类型  |  描述  |
|  :---  |  :---  |  :--- |
| symboltype    | string   | 交易对类型   |
| subsymboltype    | string   | 交易对子类型   |

### >> FuturesModel -- 期货交易对

#### Atrribute
| 属性 |  类型  |  描述  |
|  :---  |  :---  |  :--- |
| symbol    | string   | matrixdata统一交易对   |
| baseasset    | string   | 基础币种   |
| quoteasset    | string   | 计价币种   |
| contractmonth    | int   | 合约乘数   |
| contractmultiple    | int   |    |
| listedtime    | string   | 上市时间   |
| delistedtime    | string   | 退市时间   |
| deliverydate    | string   | 交割日   |
| deliverymonth    | int   | 交割月份   |
| deliveryprice    | float   | 交割价   |
| minprice    |  float  | 最小变动价位  |
| type    | SymbolTypeModel   | 交易对类型，具体属性参考 SymbolTypeModel类属性说明  |
| status    | string   | 状态   |
| displaysymbol    | string   | 交易所显示交易对   |
| tradesymbol    | string   | 交易所接口交易对   |
| exchange    | string   | 交易所   |
| latestcontract    | int   | 最新合约   |

### >> IndexModel -- 指数s交易对

#### Atrribute
| 属性 |  类型  |  描述  |
|  :---  |  :---  |  :--- |
| symbol    | string   | matrixdata统一交易对   |
| baseasset    | string   | 基础币种   |
| quoteasset    | string   | 计价币种   |
| type    | SymbolTypeModel   | 交易对类型，具体属性参考 SymbolTypeModel类属性说明  |
| status    | string   | 状态   |
| displaysymbol    | string   | 交易所显示交易对   |
| tradesymbol    | string   | 交易所接口交易对   |
| exchange    | string   | 交易所   |
| listedtime    | string   | 上市时间   |
| delistedtime    | string   | 退市时间   |
