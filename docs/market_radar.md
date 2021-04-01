# MarketRadar - 市场信号雷达模块

## 功能简介

MarketRadar是用于**实时衍生行据计算**的模块，用户可以结合Python内置诸多数学函数，对多合约价格自定义灵活的数学公式，执行高效的衍生数据计算任务。

## 加载启动

### VN Station加载

启动登录VN Station后，点击【VN Trader Pro】按钮，在配置对话框中的【上层应用】栏勾选【MarketRadar】。

### 脚本加载

在启动脚本中添加如下代码：

```
# 写在顶部
from vnpy.app.market_radar import MarketRadarApp

# 写在创建main_engine对象后
main_engine.add_app(MarketRadarApp)
```

## 启动模块

在启动模块之前，请先连接登录交易接口（连接方法详见基本使用篇的连接接口部分）。看到VN Trader主界面【日志】栏输出“合约信息查询成功”之后再启动模块，如下图所示：  

![](https://vnpy-doc.oss-cn-shanghai.aliyuncs.com/market_radar/1.png) 

成功连接交易接口后，在菜单栏中点击【功能】-> 【市场雷达】，或者点击左侧按钮栏的图标：

![](https://vnpy-doc.oss-cn-shanghai.aliyuncs.com/market_radar/2.png) 

即可进入MarketRadar的UI界面，如下图所示：

![](https://vnpy-doc.oss-cn-shanghai.aliyuncs.com/market_radar/3.png) 

## 管理雷达规则

### 添加雷达规则
在图形界面左下角的编辑区中，可以快速创建要扫描计算的雷达规则（RadarRule），如下图所示：

![](https://vnpy-doc.oss-cn-shanghai.aliyuncs.com/market_radar/4.png) 

其中，各字段的对应含义如下：  
- 名称
  - 雷达规则的名称，注意命名不能重复；
- 公式
  - 雷达规则的计算公式，支持任何Python内置数学函数；
  - 注意其中的变量只能是A、B、C、D、E（不需要都用）；
- A、B、C、D、E
  - 公式中的变量所对应的合约本地代码（vt_symbol）；
  - 收到其中任何一个合约的TICK行情推送时，会实时触发规则计算；
  - 不用的变量留空即可；
- 小数
  - 公式的最终计算结果保留多少位小数。

填写完毕后，点击【添加】按钮即可完成新规则的添加，MarketRadar会自动订阅相关合约行情并开始自动扫描计算，如下图所示。

![](https://vnpy-doc.oss-cn-shanghai.aliyuncs.com/market_radar/5.png) 

除了跨期价差这种减法求差的规则外，MarketRadar也支持金银比等跨品种价差的计算规则，如下图所示：

![](https://vnpy-doc.oss-cn-shanghai.aliyuncs.com/market_radar/6.png) 

### 修改雷达规则

对于需要调整的规则，也可以同样在左下角输入相应信息（名称请填写要修改的雷达规则名称），点击【修改】按钮即可完成修改。

### 删除雷达规则

对于不再需要的规则，可以点击监控表中最右侧的【删除】按钮来进行移除。

### 批量添加雷达规则

需要添加较多的雷达规则时，可以通过CSV文件来一次性批量导入，点击图形界面右下角的【导入CSV】按钮，在弹出的对话框中找到要导入的CSV文件后打开即可快速完成导入（右下角日志组件中有对应信息输出）。

请注意，CSV文件的格式应如下图所示，和编辑区的各字段完全一致：

![](https://vnpy-doc.oss-cn-shanghai.aliyuncs.com/market_radar/7.png) 

结合Excel的表格快速编辑功能，批量添加规则较为方便。添加成功后如下图所示：

![](https://vnpy-doc.oss-cn-shanghai.aliyuncs.com/market_radar/8.png) 

请注意，运行MarketRadar，需确保vn.py版本 ≥ 2.1.7。在目前的版本中，MarketRadar只支持雷达规则计算结果的数字显示，后续版本会进一步加入图表显示、条件提醒、策略信号订阅等功能。


