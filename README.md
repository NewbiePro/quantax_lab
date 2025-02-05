# quantax_lab
## overview structure
- quantax_lab_common
- quantax_lab_core
- quantax_lab_ucenter
- quantax_lab_wallet
- quantax_lab_market
- quantax_lab_matching
- quantax_lab_trading
- quantax_lab_admin

```mermaid
graph TD
    %% 业务接口层
    subgraph 业务接口层
        quantax_lab_gateway[API Gateway<br>统一入口/请求路由/安全校验/流量控制]
        quantax_lab_ucenter[Ucenter Module<br>用户中心<br>认证/授权/安全]
        quantax_lab_trading[Trading Module<br>交易接口<br>现货/合约交易API]
    end

    %% 业务服务层
    subgraph 业务服务层
        quantax_lab_wallet[Wallet Module<br>钱包服务<br>充提币/地址管理]
        quantax_lab_market[Market Module<br>行情服务<br>K线/深度/Ticker]
        quantax_lab_matching[Matching Module<br>交易撮合引擎<br>订单簿/撮合逻辑]
        quantax_lab_event_bus[Event Bus<br>消息总线/Kafka]
    end

    %% 基础设施层
    subgraph 基础设施层
        %% common 子模块
        subgraph quantax_lab_common[Common Module<br>公共组件]
            quantax_lab_common_cache[Cache Module<br>缓存]
            quantax_lab_common_utils[Utilities Module<br>工具类]
        end
        quantax_lab_core[Core Module<br>配置类/Kafka配置/数据库配置等]
        quantax_lab_monitor[Monitor Module<待定><br>监控/日志收集/告警]
    end

    %% 后台管理平台
    subgraph 后台管理平台
        quantax_lab_admin[Admin Module<br>后台管理<br>运营/风控/审计]
    end

%% 依赖关系
    quantax_lab_gateway -- "调用用户认证接口" --> quantax_lab_ucenter
    quantax_lab_gateway -- "转发交易请求" --> quantax_lab_trading

    quantax_lab_trading -- "获取用户信息" --> quantax_lab_ucenter
    quantax_lab_trading -- "获取行情数据" -->  quantax_lab_market
    quantax_lab_trading -- "获取撮合数据" --> quantax_lab_matching
    quantax_lab_trading -- "查询钱包状态" -->  quantax_lab_wallet

    quantax_lab_matching -- "异步撮合成功事件" --> quantax_lab_event_bus
    quantax_lab_wallet -- "资金变更事件" --> quantax_lab_event_bus
    quantax_lab_market -- "市场变动事件" --> quantax_lab_event_bus

    quantax_lab_event_bus -- "通知资金变更" --> quantax_lab_wallet
    quantax_lab_event_bus -- "通知市场行情更新" --> quantax_lab_market
    quantax_lab_event_bus -- "通知撮合引擎更新" --> quantax_lab_matching


    quantax_lab_wallet --> quantax_lab_core
    quantax_lab_market --> quantax_lab_core
    quantax_lab_matching --> quantax_lab_core
    quantax_lab_core --> quantax_lab_common


    quantax_lab_admin --> quantax_lab_core
    quantax_lab_admin --> quantax_lab_ucenter
```



