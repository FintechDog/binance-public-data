## 安装依赖

`uv sync`

该命令会在 `.venv` 中创建虚拟环境并安装依赖。脚本也可用 `uv run` 运行，例如 `uv run download-kline.py -t spot`。

## 运行脚本

`export STORE_DIRECTORY=<你期望的路径>`

这里配置的是下载数据的默认存储目录，可通过传入参数覆盖（示例见下）。

### 下载 K 线

`python3 download-kline.py -t <市场类型>` <br/>

运行该命令会下载 **spot**（现货）、**USD-M 合约** 或 **COIN-M 合约** 中，全部交易对、全部周期、**2020-01-01** 起所有可用的月度和日度 K 线数据。

#### 带参数运行

以下是运行 `download-kline.py` 时可用的参数。<br>
部分参数未声明时带有默认值。

| 参数 | 说明 | 默认值 | 是否必填 |
| :---------------: | ---------------- | :----------------: | :----------------: |
| -t              | 市场类型：**spot**、**um**（USD-M 合约）、**cm**（COIN-M 合约） | spot | 是 |
| -s              | 单个**交易对**或多个**交易对**，以空格分隔 | 全部交易对 | 否 |
| -i              | 单个 K 线**周期**或多个**周期**，以空格分隔      | 全部周期 | 否 |
| -y              | 单个**年份**或多个**年份**，以空格分隔| 2020 年至当前年份的全部可用年份 | 否 |
| -m              | 单个**月份**或多个**月份**，以空格分隔 | 全部可用月份 | 否 |
| -d              | 单个**日期**或多个**日期**，以空格分隔    | 2020-01-01 起的全部可用日期 | 否 |
| -startDate      | 下载的**起始日期**，格式 [YYYY-MM-DD]    | 2020-01-01 | 否 |
| -endDate        | 下载的**结束日期**，格式 [YYYY-MM-DD]     | 当前日期 | 否 |
| -skip-monthly   | 设为 1 跳过月度数据 | 0 | 否 |
| -skip-daily     | 设为 1 跳过日度数据 | 0 | 否 |
| -folder         | 存放下载数据的**目录**    | 当前目录 | 否 |
| -c              | 设为 1 下载**校验和文件** | 0 | 否 |
| -h              | 显示帮助信息| - | 否 |

#### 示例

例如下载 ETHUSDT、BTCUSDT、BNBBUSD 现货 1 周周期的 K 线，年份 2020、月份 2 月和 12 月，并带校验和文件：<br/>
`python3 download-kline.py -t spot -s ETHUSDT BTCUSDT BNBBUSD -i 1w -y 2020 -m 02 12 -c 1`

例如下载全部交易对 2021-01-01 至 2021-02-02 的 USD-M 合约日度 1 分钟 K 线：
`python3 download-kline.py -t um -i 1m -skip-monthly 1 -startDate 2021-01-01 -endDate 2021-02-02`

### 下载逐笔成交

`python3 download-trade.py -t <市场类型>` <br/>

运行该命令会下载 **spot**（现货）、**USD-M 合约** 或 **COIN-M 合约** 中，全部交易对、**2020-01-01** 起所有可用的月度和日度逐笔成交数据。

#### 带参数运行

以下是运行 `download-trade.py` 时可用的参数。<br>
部分参数未声明时带有默认值。

| 参数 | 说明 | 默认值 | 是否必填 |
| :---------------: | ---------------- | :----------------: | :----------------: |
| -t              | 市场类型：**spot**、**um**（USD-M 合约）、**cm**（COIN-M 合约） | spot | 是 |
| -s              | 单个**交易对**或多个**交易对**，以空格分隔 | 全部交易对 | 否 |
| -y              | 单个**年份**或多个**年份**，以空格分隔| 2020 年至当前年份的全部可用年份 | 否 |
| -m              | 单个**月份**或多个**月份**，以空格分隔 | 全部可用月份 | 否 |
| -d              | 单个**日期**或多个**日期**，以空格分隔    | 2020-01-01 起的全部可用日期 | 否 |
| -startDate      | 下载的**起始日期**，格式 [YYYY-MM-DD]    | 2020-01-01 | 否 |
| -endDate        | 下载的**结束日期**，格式 [YYYY-MM-DD]     | 当前日期 | 否 |
| -skip-monthly   | 设为 1 跳过月度数据 | 0 | 否 |
| -skip-daily     | 设为 1 跳过日度数据 | 0 | 否 |
| -folder         | 存放下载数据的**目录**    | 当前目录 | 否 |
| -c              | 设为 1 下载**校验和文件** | 0 | 否 |
| -h              | 显示帮助信息| - | 否 |

#### 示例

例如下载 ETHUSDT、BTCUSDT、BNBBUSD 现货逐笔成交数据，年份 2020、月份 2 月和 12 月，并带校验和文件：<br/>
`python3 download-trade.py -t spot -s ETHUSDT BTCUSDT BNBBUSD -y 2020 -m 02 12 -c 1`

例如下载全部交易对 2021-01-01 至 2021-02-02 的 USD-M 合约日度逐笔成交数据：
`python3 download-trade.py -t um -skip-monthly 1 -startDate 2021-01-01 -endDate 2021-02-02`

### 下载聚合成交

`python3 download-aggTrade.py -t <市场类型>` <br/>

运行该命令会下载 **spot**（现货）、**USD-M 合约** 或 **COIN-M 合约** 中，全部交易对、**2020-01-01** 起所有可用的月度和日度聚合成交数据。

#### 带参数运行

以下是运行 `download-aggTrade.py` 时可用的参数。<br>
部分参数未声明时带有默认值。

| 参数 | 说明 | 默认值 | 是否必填 |
| :---------------: | ---------------- | :----------------: | :----------------: |
| -t              | 市场类型：**spot**、**um**（USD-M 合约）、**cm**（COIN-M 合约） | spot | 是 |
| -s              | 单个**交易对**或多个**交易对**，以空格分隔 | 全部交易对 | 否 |
| -y              | 单个**年份**或多个**年份**，以空格分隔| 2020 年至当前年份的全部可用年份 | 否 |
| -m              | 单个**月份**或多个**月份**，以空格分隔 | 全部可用月份 | 否 |
| -d              | 单个**日期**或多个**日期**，以空格分隔    | 2020-01-01 起的全部可用日期 | 否 |
| -startDate      | 下载的**起始日期**，格式 [YYYY-MM-DD]    | 2020-01-01 | 否 |
| -endDate        | 下载的**结束日期**，格式 [YYYY-MM-DD]     | 当前日期 | 否 |
| -skip-monthly   | 设为 1 跳过月度数据 | 0 | 否 |
| -skip-daily     | 设为 1 跳过日度数据 | 0 | 否 |
| -folder         | 存放下载数据的**目录**    | 当前目录 | 否 |
| -c              | 设为 1 下载**校验和文件** | 0 | 否 |
| -h              | 显示帮助信息| - | 否 |

#### 示例

例如下载 ETHUSDT、BTCUSDT、BNBBUSD 现货聚合成交数据，年份 2020、月份 2 月和 12 月，并带校验和文件：<br/>
`python3 download-aggTrade.py -t spot -s ETHUSDT BTCUSDT BNBBUSD -y 2020 -m 02 12 -c 1`

例如下载全部交易对 2021-01-01 至 2021-02-02 的 USD-M 合约日度聚合成交数据：
`python3 download-aggTrade.py -t um -skip-monthly 1 -startDate 2021-01-01 -endDate 2021-02-02`

### 仅期货数据

以下 3 个脚本仅用于期货 K 线数据。运行这些命令会下载 **USD-M 合约** 或 **COIN-M 合约** 中，全部交易对、**2020-01-01** 起所有可用的月度和日度 indexPriceKlines（指数价格 K 线）、markPriceKlines（标记价格 K 线）或 premiumPriceKlines（溢价价格 K 线）。

`python3 download-futures-indexPriceKlines.py -t <市场类型>` <br/>
`python3 download-futures-markPriceKlines.py -t <市场类型>` <br/>
`python3 download-futures-premiumPriceKlines.py -t <市场类型>`

#### 带参数运行

以下是运行这些脚本时可用的参数。<br>
**`-t`（类型）是必填参数，只包含两种期货类型：`um`、`cm`**。部分参数未声明时带有默认值。

| 参数 | 说明 | 默认值 | 是否必填 |
| :---------------: | ---------------- | :----------------: | :----------------: |
| -t              | 市场类型：**um**（USD-M 合约）、**cm**（COIN-M 合约）| - | 是 |
| -s              | 单个**交易对**或多个**交易对**，以空格分隔 | 全部交易对 | 否 |
| -i              | 单个 K 线**周期**或多个**周期**，以空格分隔      | 全部周期 | 否 |
| -y              | 单个**年份**或多个**年份**，以空格分隔| 2020 年至当前年份的全部可用年份 | 否 |
| -m              | 单个**月份**或多个**月份**，以空格分隔 | 全部可用月份 | 否 |
| -d              | 单个**日期**或多个**日期**，以空格分隔    | 2020-01-01 起的全部可用日期 | 否 |
| -startDate      | 下载的**起始日期**，格式 [YYYY-MM-DD]    | 2020-01-01 | 否 |
| -endDate        | 下载的**结束日期**，格式 [YYYY-MM-DD]     | 当前日期 | 否 |
| -skip-monthly   | 设为 1 跳过月度数据 | 0 | 否 |
| -skip-daily     | 设为 1 跳过日度数据 | 0 | 否 |
| -folder         | 存放下载数据的**目录**    | 当前目录 | 否 |
| -c              | 设为 1 下载**校验和文件** | 0 | 否 |
| -h              | 显示帮助信息| - | 否 |

例如下载期货 BTCUSDT 的 USD-M indexPriceKlines（指数价格 K 线）：
`python3 download-futures-indexPriceKlines.py -t um -s BTCUSDT`

例如下载 ETHUSDT、BTCUSDT、BNBUSDT 的 USD-M markPriceKlines（标记价格 K 线）1 周周期数据，年份 2020、月份 2 月和 12 月，并带校验和文件：<br/>
`python3 download-futures-markPriceKlines.py -t um -s ETHUSDT BTCUSDT BNBUSDT -i 1w -y 2020 -m 02 12 -c 1`

例如下载全部交易对 2021-01-01 至 2021-02-02 的 COIN-M premiumPriceKlines（溢价价格 K 线）日度 1 分钟数据：
`python3 download-futures-premiumPriceKlines.py -t cm -skip-monthly 1 -i 1m  -startDate 2021-01-01 -endDate 2021-02-02`
