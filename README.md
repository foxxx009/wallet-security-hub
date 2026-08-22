# Web3 Wallet Security Hub

一个入口搞定钱包安全的三合一纯前端工具，**无后端、无 KYC、无平台抽成**，所有付费以 USDC 直接结算至 `0x2409b47a530be3831158f10b08ac93f7d08c1ff2`。

> 由 SafeScan + ApprovalGuard 整合而来，并新增「合约黑名单查询」模块。

## 三个模块

| 模块 | 功能 | 免费 | 付费解锁 |
|---|---|---|---|
| 🔍 地址扫描 (SafeScan) | 合约/EOA、余额、首笔交易、代币识别 | ✅ 基础扫描 | **$0.05 USDC** → 深度报告（权限审计 + 流动性锁 + 持仓集中度 + rug 风险评分 + 多链对比 + JSON 导出） |
| 🛡️ 授权巡检 (Approval Guard) | 查 ERC-20/721 危险授权（无限授权 / 未知 spender） | ✅ 列表 | **$0.02 USDC** → 生成 `approve(spender,0)` 撤销交易（raw tx + EIP-681 扫码撤销 + 批量清单） |
| ⚫ 合约黑名单 (Blacklist) | 代币/合约地址比对已知 scam 特征 + 权限后门 | ✅ 特征速查 | **$0.03 USDC** → 完整风险报告（蜜罐特征 + 权限后门 + 已知命中 + 风险评分 + JSON 导出） |
| ⛽ Gas 估算 (Gas) | 实时 Gas 价格、常见操作成本、**交易预审**（输入 to + data 估算 gas limit 与费用） | ✅ 全部免费 | 引流工具，不收费，导流向上方付费模块 |

## 合约黑名单数据说明

- **内置可信库**：收录公开可验证的知名 honeypot / 诈骗代币与恶意合约地址（如 Squid Game honeypot、伪造 OpenAI/ChatGPT 代币、approval drainer 等），均来自社区公开报告。
- **用户本地黑名单**：每个访客可在「合约黑名单」Tab 内一键把当前地址「加入我的黑名单」，仅存于本机浏览器（localStorage），**不联网、不上传**。你积累的黑名单只对你自己可见。
- 命中内置或本地黑名单时，免费速查即显示命中详情与来源说明。

## 技术

- 纯静态 HTML + 原生 JS，**零依赖、零构建**。
- 链上数据通过公共 RPC 直查（`eth_call` / `eth_getLogs` / `eth_getCode` / `eth_getTransactionReceipt`），多 RPC fallback，**不依赖任何 explorer API**（Basescan/Etherscan V1 已废弃）。
- 付费校验：用户钱包向本站收款地址打 USDC（Base 链），前端用 `eth_getTransactionReceipt` + ERC-20 Transfer 事件 topic 校验 `topics[2]==0x2409…c1ff2` 且金额达标，**无服务器参与**。
- 支持以太坊、Base、Arbitrum、BNB Chain、Polygon 五条链。
- 中 / EN 双语，渠道归因（`?src=`）、Cloudflare Web Analytics 埋点（付费转化可追踪来源）。

## 使用

打开 **https://foxxx009.github.io/wallet-security-hub/** ，选择对应 Tab，粘贴地址即可。

⚠️ 评分为基于公开链上数据的启发式判断，不构成投资建议，不能替代专业审计。

## 收款

所有模块共享同一地址：

```
0x2409b47a530be3831158f10b08ac93f7d08c1ff2   (USDC on Base)
```
