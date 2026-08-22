# Web3 Wallet Security Hub

A single-entry wallet-security toolkit — three tools in one client-side page. **No backend, no KYC, no platform fee.** All paid unlocks settle in USDC directly to `0x2409b47a530be3831158f10b08ac93f7d08c1ff2`.

> Built by merging SafeScan + ApprovalGuard, then adding four more modules — Contract Blacklist, Gas Estimator, Contract Similarity, and Tx Simulate — into one page with six tabs.

## Six modules

| Module | What it does | Free | Paid unlock |
|---|---|---|---|
| 🔍 Address Scan (SafeScan) | Contract/EOA, balances, first-tx age, token identification | ✅ Basic scan | **$0.05 USDC** → deep report (permission audit + liquidity lock + holder concentration + rug risk score + multi-chain compare + JSON export) |
| 🛡️ Approval Guard | Find dangerous ERC-20/721 approvals (unlimited / unknown spender) | ✅ List | **$0.02 USDC** → generate `approve(spender,0)` revoke tx (raw tx + EIP-681 scan-to-revoke + batch list) |
| ⚫ Contract Blacklist | Match token/contract against known scam traits + permission backdoors | ✅ Trait lookup | **$0.03 USDC** → full risk report (honeypot traits + permission backdoors + known hits + risk score + JSON export) |
| ⛽ Gas Estimator | Live gas price, common-op cost, **tx pre-check** (estimate gas for to + data) | ✅ Fully free | Lead-in tool, no charge — funnels to the paid modules above |
| 🔬 Contract Similarity | Fetch bytecode, compare to known malicious templates via **function-selector + opcode similarity** | ✅ Overview (top similarity + template name) | **$0.04 USDC** → full comparison report (all-template similarity breakdown + save as local baseline + JSON export) |
| 🎯 Tx Simulate | Dry-run an unsigned tx (from/to/data/value) on-chain, **free to see if it reverts** | ✅ Pre-exec result (revert? + target reputation) | **$0.06 USDC** → post-execution impact report (native balance change + USDC/USDT balance + allowance change + target blacklist hit + verdict + JSON export) |

## Contract blacklist data

- **Built-in trusted library**: known, publicly verifiable honeypot / scam tokens and malicious contracts (e.g. Squid Game honeypot, fake OpenAI/ChatGPT tokens, approval drainers) — all sourced from public community reports.
- **User local blacklist**: each visitor can one-click "add to my blacklist" for any address inside the Contract Blacklist tab. Stored only in the local browser (localStorage) — **no network, no upload**. Your blacklist is visible to you only.
- On a hit (built-in or local), the free lookup already shows the hit details and source note.

## Tech

- Pure static HTML + vanilla JS, **zero dependencies, zero build**.
- On-chain data queried directly via public RPC (`eth_call` / `eth_getLogs` / `eth_getCode` / `eth_getTransactionReceipt`), with multi-RPC fallback. **Does not depend on any explorer API** (Basescan/Etherscan V1 are deprecated).
- Payment verification: the user's wallet sends USDC (Base chain) to the site's receiving address; the frontend verifies via `eth_getTransactionReceipt` + the ERC-20 Transfer event topic, checking `topics[2]==0x2409…c1ff2` and the amount — **no server involved**.
- Supports Ethereum, Base, Arbitrum, BNB Chain, and Polygon.
- Bilingual (zh / EN), with channel attribution (`?src=`) and Cloudflare Web Analytics (paid conversions are source-trackable).

## Usage

Open **https://foxxx009.github.io/wallet-security-hub/**, pick a tab, paste an address.

⚠️ Scores are heuristic judgments based on public on-chain data. Not investment advice, not a substitute for a professional audit.

## Payments

All modules share one address:

```
0x2409b47a530be3831158f10b08ac93f7d08c1ff2   (USDC on Base)
```
