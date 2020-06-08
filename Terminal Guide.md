# Terminal 使用说明

## 一. 安装

【Windows】：双击安装包 [Sam Terminal.exe] 安装，可自定义安装位置。

【MacOs】：双击安装包 [Sam Termianl.dmg] 安装。

## 二. 启动

双击程序启动 Sam Terminal，输入账号密码登录。（账号可从 [Samdata官网](https://www.samdata.trade/) 注册），成功登录出现欢迎页面。 

## 三. 使用说明

运行回测的步骤：

   1. 首先在 [官网商城](https://www.samdata.trade/shop) 中购买了数据；
   2. 登录 Terminal 终端，在数据文件模块，点击下载文件；或者，在数据同步模块，点击需要同步的数据；
   3. 文件下载或者同步完成后，编写策略；
   4. 运行回测，查看回测结果。

**注：在运行回测之前要确保数据文件或数据库存在，否则无法运行回测。**

**数据来源于官网商城购买的数据：**

![官网商城数据](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/170839-257418.png)

## 四. 回测示例

### 1. 登录Terminal，检查订单数据

登录终端账号，并在官网中检查是否存在有效的订单数据（示例中购买了2019-01~2019-04的期货K线数据）

![登录](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/144842-766561.png)

![订单](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/145848-87305.png)

### 2. 下载文件

在数据文件页面中，会显示您在官网已购买的订单数据，然后点击下载文件。**数据文件是运行回测的数据源之一**。

- 查看未下载的数据文件：

![未下载数据](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/150243-286405.png)

- 查看已下载的数据文件：

![已下载数据](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/150710-886648.png)  

### 3. 同步数据

在数据同步页面，可将用户在官网购买的数据同步至用户配置的数据库中。**数据库的数据也可作为运行回测的数据源之一**。

免费的数据包可免费同步至服务器的数据库中，付费的数据包需要在[官网商城](https://www.samdata.trade/shop)中购买方可同步。

同步状态有：未同步，正在同步，待同步，同步成功，同步失败；

![1591600428995](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/151455-870342.png)

### 4. 策略编写

等待数据下载或数据同步完成后，编写策略，运行回测。

编写策略流程：新建策略 -> 编写策略 -> 运行回测，示例如下：（示例已下载数据文件）

- #### 新建策略
  
  ![新建策略](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/154001-778738.png)

- #### 编写策略
  
  编写策略页面左边是代码目录，demo为示例代码目录，code为存放代码目录。中间是编辑策略代码区域。右边是API文档区域，点击右上角的"API文档"可关闭文档，也可拖动紫色边栏拉伸API文档区域大小。
  
  运行策略前，检查回测开始时间和结束时间的数据是否存在。

  ![编辑策略](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/155254-535749.png)

- #### 运行回测

  运行策略时，检查运行目录路径是否正确。

  运行命令：python xxx.py

## 五. 回测报告

点击回测次数可查看历史回测列表，点击回测结果可查看对应的回测详情：

![回测列表](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/171312-840726.png)   

![回测详情](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/171352-339536.png)

示例回测结果如下：

![示例回测结果](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/162233-357247.png) ![1591607099362](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/170459-836046.png) 

可查看具体的盈亏分析，交易记录，持仓历史，回测日志：

![盈亏分析](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/170536-636796.png)

![交易记录](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/170636-666823.png)

![持仓历史](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/170738-473023.png)  

![回测日志](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/170914-5668.png)

## 六. 用户中心和配置中心

- 用户中心
  
  查看账号，修改密码，退出登录功能。

  ![用户中心](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/171156-172116.png) 

- 配置中心
  
  服务配置：支持用户自定义配置服务，目前支持：VSCode 服务地址配置，Terminal 业务中心服务地址配置，数据同步服务 API 地址配置，回测计算服务地址配置。

  ![服务配置](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/171013-41135.png) 

  系统配置：

  ![系统配置](https://raw.githubusercontent.com/SmartAssetManager/SAM-Learn/master/images202006/08/171219-290747.png) 