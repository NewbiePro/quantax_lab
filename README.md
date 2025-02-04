# quantax_lab
## overview structure

# quantax_lab_common
## this module is used to store the common code for other modules
# quantax_lab_core
## this module is used to store the core code for other modules
```mermaid
graph TD
    subgraph 基础设施层
        crypto_lab_common[Common Module<br>通用工具类、DTO、异常处理等]
        crypto_lab_core[Core Module<br>核心配置、数据库基础、消息队列等]
    end
  
    subgraph 业务服务层
        crypto_lab_ucenter[Ucenter Module<br>用户中心<br>认证/授权/安全]
        crypto_lab_wallet[hi Module<br>钱包服务<br>充提币/地址管理]
        crypto_lab_market[Market Module<br>行情服务<br>K线/深度/Ticker]
        crypto_lab_matching[Matching Module<br>撮合引擎<br>订单簿/撮合逻辑]
    end
  
    subgraph 业务接口层
        crypto_lab_trading[Trading Module<br>交易接口<br>现货/合约交易API]
    end
  
    subgraph 管理端
        crypto_lab_admin[Admin Module<br>后台管理<br>运营/风控/审计]
    end
  
    %% 依赖关系
    crypto_lab_core --> crypto_lab_common
    crypto_lab_ucenter --> crypto_lab_core
    crypto_lab_wallet --> crypto_lab_core
    crypto_lab_market --> crypto_lab_core
    crypto_lab_matching --> crypto_lab_core
    crypto_lab_trading --> crypto_lab_ucenter
    crypto_lab_trading --> crypto_lab_market
    crypto_lab_trading --> crypto_lab_matching
    crypto_lab_trading --> crypto_lab_wallet
    crypto_lab_admin --> crypto_lab_core
    crypto_lab_admin --> crypto_lab_ucenter
```

# quantax_lab_market
## 行情模块
# quantax_lab_trading
## 交易模塊包括合約以及現貨
# quantax_lab_ucenter
## 用戶中心模塊

# quantax_lab_wallet
## 錢包模塊
# quantax_lab_matching
## 交易撮合模塊

-- admin --
# quantax_lab_admin
## 后台管理端

