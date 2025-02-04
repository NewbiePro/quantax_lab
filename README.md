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
    subgraph 基础设施层
        quantax_lab_common[Common Module<br>通用工具类、Bean类[DTO、VO、CONSTANT etc]、Mapper、CACHE]
        quantax_lab_core[Core Module<br>配置类、数据库基础、消息队列等]
    end
  
    subgraph 业务服务层
        quantax_lab_ucenter[Ucenter Module<br>用户中心<br>认证/授权/安全]
        quantax_lab_wallet[Wallet Module<br>钱包服务<br>充提币/地址管理]
        quantax_lab_market[Market Module<br>行情服务<br>K线/深度/Ticker]
        quantax_lab_matching[Matching Module<br>交易撮合引擎<br>订单簿/撮合逻辑]
    end
  
    subgraph 业务接口层
        quantax_lab_trading[Trading Module<br>交易接口<br>现货/合约交易API]
    end
  
    subgraph 后台管理端
        quantax_lab_admin[Admin Module<br>后台管理<br>运营/风控/审计]
    end
  
    %% 依赖关系
    quantax_lab_core --> quantax_lab_common
    quantax_lab_ucenter --> quantax_lab_core
    quantax_lab_wallet --> quantax_lab_core
    quantax_lab_market --> quantax_lab_core
    quantax_lab_matching --> quantax_lab_core
    quantax_lab_trading --> quantax_lab_ucenter
    quantax_lab_trading --> quantax_lab_market
    quantax_lab_trading --> quantax_lab_matching
    quantax_lab_trading --> quantax_lab_wallet
    quantax_lab_admin --> quantax_lab_core
    quantax_lab_admin --> quantax_lab_ucenter
```

