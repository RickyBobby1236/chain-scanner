# SWEEP ENGINE V15

**Live:** https://rickybobby1236.github.io/chain-scanner

Multi-chain wallet portfolio scanner, sweep queue, contract verifier, and AI agent deploy tool. Single-file architecture — no build step, no npm, no framework.

-----

## Features

### ⚡ Connect

Connect via MetaMask, Trust, Coinbase, Rabby, OKX, FoxWallet, Phantom, Exodus, CoinWallet, Zerion, or any injected Web3 wallet. Paste an EVM address for read-only scanning. Solana addresses supported separately via Solscan V2.

### 💰 Money Finder

Scans 20+ DeFi protocols for unclaimed or stuck value — Uniswap V3 fees, DAI DSR, Morpho, Gnosis Safe, Lido withdrawals, NFT royalties, Compound, Convex, GMX, Aerodrome, and more. Ranks results by USD and shows exact recovery steps.

### 🔐 Safe Exec

Gnosis Safe executor. Load any Safe by address, inspect the tx queue, verify threshold, build `execTransaction` calldata, and send directly from your connected wallet. Pre-loaded with nonce 137 for the queued wstETH deposit tx.

### 🔍 Scan

Parallel EVM scan across 13 chains. Fetches native balances, ERC-20 tokens, LP positions (Uniswap V2/V3, SushiSwap, PancakeSwap, Camelot, QuickSwap, Aerodrome), staked positions (Lido, Rocket Pool, Aave, Compound, Convex, GMX, Yearn), pending rewards, and NFT holdings with live Reservoir floor prices.

### ✅ Contract Verify

OKLink API integration for full contract verification:

- Submit Solidity source or Standard JSON input
- Auto-polls every 5s until verified or failed
- Proxy contract detection and verification
- Fetch existing source info (auto-fills compiler fields)
- Hardhat, Foundry, and Truffle config snippets (auto-updates to selected chain)

### 🪙 Tokens / 💧 Liq Pools / 🖼 NFTs / 💰 Sweep

Post-scan tabs showing ERC-20 balances with USD values, LP positions, NFT grid with floor prices, and a full sweep queue combining history, staked, LP, and reward positions into one executable batch.

### ◎ Solana

SOL balance, SPL token accounts, staked SOL, and recent transactions via Solscan V2 API.

### 🦊 MetaMask

Full MetaMask feature breakdown with cross-reference table (Sweep Engine vs MetaMask capabilities), deep links to Buy, Earn, Swaps, Card, Perps, RWAs, Prediction Markets, and SDK docs. Live scan data integration shows your portfolio stats inline.

### 🚀 Agents

GitHub token-gated auto-deploy for AGENTS.md, CLAUDE.md, and skill files across 3 repos (ScoutAI, Chain Scanner, Satoshi Puzzle Art). Commits all 17 files via GitHub API — no copy-paste needed.

### 📡 RPC Explorer

1000+ EVM chains from Chainlist.org with privacy tracking filters (no-track / limited / tracked), TVL sort, WSS toggle, testnet toggle, and one-tap “USE IN SCAN” to override any chain’s RPC endpoint live.

-----

## Supported Chains

|Chain    |Symbol|Chain ID|Scan                    |
|---------|------|--------|------------------------|
|Ethereum |ETH   |1       |✅ Full                  |
|BNB Chain|BNB   |56      |✅ Full                  |
|Arbitrum |ETH   |42161   |✅ Full                  |
|Polygon  |POL   |137     |✅ Full                  |
|Optimism |ETH   |10      |✅ Full                  |
|Base     |ETH   |8453    |✅ Full                  |
|Avalanche|AVAX  |43114   |✅ Full                  |
|Linea    |ETH   |59144   |✅ Full                  |
|Gnosis   |xDAI  |100     |✅ Full                  |
|Ink      |ETH   |57073   |✅ Full                  |
|Plasma   |ETH   |1101    |✅ Full                  |
|Fantom   |FTM   |250     |✅ Full                  |
|Sonic    |S     |146     |✅ Full                  |
|Aptos    |APT   |—       |🔗 Display only (non-EVM)|
|Solana   |SOL   |—       |✅ Full (separate tab)   |

-----

## Architecture

Single-file `index.html` — all HTML, CSS, and JS inline. Deployed via GitHub Pages. No Node, no npm, no build pipeline.

Owner deploys from iPhone/Android via the GitHub web editor. Edit `index.html` → commit to `main` → live in ~60 seconds.

**Always output the complete `index.html`.** No partial diffs.

-----

## API Keys

|Service               |Usage                                                         |
|----------------------|--------------------------------------------------------------|
|Etherscan (shared key)|ETH, BSC, ARB, POLY, OP, BASE, AVAX, LINEA, GNOSIS, FTM, SONIC|
|Solscan V2            |SOL balance, SPL tokens, staking, transactions                |
|CoinGecko (public)    |Token prices                                                  |
|Reservoir (public)    |NFT floor prices                                              |
|OKLink                |Contract verification (user-provided key)                     |

API keys are stored in the source for EVM/Solana scanning. OKLink key is entered by the user in the Verify tab.

-----

## Skills

|Domain                    |Path                              |
|--------------------------|----------------------------------|
|Stack & coding conventions|`.agents/skills/stack/SKILL.md`   |
|Deploy workflow           |`.agents/skills/deploy/SKILL.md`  |
|Security                  |`.agents/skills/security/SKILL.md`|

-----

## Version History

- **V15** — Added Fantom (FTM), Sonic (S), Aptos display card
- **V14** — Added OKLink Contract Verify tab, MetaMask integration tab, AGENTS.md auto-deploy tab
- **V13** — OKLink verify tab (standalone)
- **V12** — Money Finder, Gnosis Safe Executor, Solana (Solscan V2), RPC Explorer, Tokens, LP Pools, staking detection
- **V7** — Initial multi-chain scanner, NFTs, Sweep queue
