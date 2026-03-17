# SWEEP ENGINE V18

**Live:** https://rickybobby1236.github.io/chain-scanner

Multi-chain wallet portfolio scanner, intel engine, bounty hunter, contract verifier, and AI agent deploy tool. Single-file architecture — no build step, no npm, no framework.

-----

## What’s New in V18 — All Holes Fixed

16 bugs and stubs identified in V17 audit, all resolved:

|# |Fix                                   |Detail                                                                     |
|--|--------------------------------------|---------------------------------------------------------------------------|
|1 |Money Finder implemented              |Was a stub — now fully scans 11 protocols live                             |
|2 |Gnosis Safe Executor implemented      |Was a stub — now loads Safe, queries queue, builds calldata, executes      |
|3 |ABI lookup extended to all chains     |Was ETH-only — now runs per-chain with each chain’s own explorer           |
|4 |Bounty Engine 2 rate bomb fixed       |Capped to 10 blocks, max 5 receipt checks per block                        |
|5 |Social proof extended to all chains   |Was ETH-only — now runs on every active chain                              |
|6 |Bounty SPEED UP EIP-1559 fixed        |Was sending legacy gasPrice — now sends maxFeePerGas + maxPriorityFeePerGas|
|7 |Sonic bounty zero address fixed       |Replaced with real Shadow DEX + Beethoven-x addresses                      |
|8 |Approval scan block range fixed       |Was fromBlock=0 (genesis) — now rolling 2-year window per chain            |
|9 |Social proof sample quality note      |Documented — any overlap qualifies, 70% success threshold                  |
|10|Pending pool warning added            |Shows clear message when RPC doesn’t expose mempool                        |
|11|USD value on incoming transfers       |Incoming ERC-20s now show USD value via CoinGecko token price              |
|12|ERC-20 scan all chains                |Was limited to 6 chains — now runs on all 13 active chains                 |
|13|NFT scan multi-chain                  |Was ETH-only — now scans NFTs on all active chains                         |
|14|Dead variable removed                 |`currentBlock` in bounty Engine 1 was declared but never used              |
|15|Intel action bar display bug          |Double `display:` declaration fixed                                        |
|16|Money Finder button enabled on connect|Button now correctly enables when wallet connects                          |

-----

## Features

### ⚡ Connect

11 wallet types: MetaMask, Trust, Coinbase, Rabby, OKX, FoxWallet, Phantom, Exodus, CoinWallet, Zerion, Any injected wallet. Paste EVM address for read-only scan. Solana supported separately via Solscan V2.

### 💰 Money Finder

Live protocol scanning for unclaimed and stuck value. 11 protocols fully implemented:

|Protocol                |Chain|Type     |
|------------------------|-----|---------|
|CowSwap Vault           |ETH  |CLAIMABLE|
|DAI Savings Rate (DSR)  |ETH  |YIELD    |
|Lido Withdrawal Queue   |ETH  |CLAIMABLE|
|Morpho Blue Rewards     |ETH  |CLAIMABLE|
|Compound v2 cETH        |ETH  |YIELD    |
|Convex CRV Rewards      |ETH  |CLAIMABLE|
|GMX Staking Rewards     |ARB  |CLAIMABLE|
|Aerodrome Rewards       |BASE |CLAIMABLE|
|Aave v3 Rewards         |ETH  |CLAIMABLE|
|NFT Royalties (Manifold)|ETH  |CLAIMABLE|
|Uniswap V3 LP Fees      |ETH  |LP_FEES  |

Results ranked by USD value. One-tap execute per item.

### 🔐 Gnosis Safe Executor

Full implementation — not a stub:

- Load any Safe by address + chain
- Reads nonce, threshold, ETH balance, owner list via RPC
- Detects if connected wallet is an owner
- Loads queued txs from Safe Transaction Service API (ETH, ARB, POLY, OP, BASE)
- Click any queued tx to load into builder
- Builds full `execTransaction` calldata (ABI-encoded)
- Sends to wallet for signing via `eth_sendTransaction`
- Pre-loaded with nonce 137 wstETH deposit tx

### 🔍 Scan

Parallel EVM scan across 13 chains. Fetches native balances, ERC-20 tokens (all chains), LP positions (Uni V2/V3, Sushi, Pancake, Camelot, Quickswap, Aerodrome), staked positions (Lido, Rocket Pool, Aave, Compound, Convex, GMX, Yearn), pending rewards, and NFTs (all chains) with Reservoir floor prices.

### ✅ Contract Verify

OKLink 5-endpoint integration: submit source, poll result, verify proxy, poll proxy result, fetch source info. Auto-fills compiler fields. Hardhat/Foundry/Truffle snippets per chain.

### 🔴 Intel Engine

Auto-runs after every scan — 6 phases, silent until complete:

|Phase|What it does                                                                                        |
|-----|----------------------------------------------------------------------------------------------------|
|1    |ABI lookup + contract name resolution (all chains)                                                  |
|2    |Verification status — ⚠ badge on unverified contracts                                               |
|3    |Token approvals — finds active approvals across all chains, separates ∞ from limited, one-tap REVOKE|
|4    |Internal transactions — value moved via contract calls                                              |
|5    |Incoming ERC-20 transfers — tokens received with no outgoing tx, with USD value                     |
|6    |Social proof — similar wallet fingerprint scoring, honeypot detection, proxy verification           |

**Social Proof (Phase 6):** For each unverified contract, pulls recent callers, scores by overlap with your contract interaction set, measures success rate and value returned, detects honeypots (sweepable + zero value returned), verifies EIP-1967 proxy implementations. TRUSTED contracts auto-queue to sweep if sweepable.

**Contract tab badges:** `✓ verified` · `⚠ UNVERIFIED` · `🤝 87%` · `⚠ HONEYPOT` · `LOW TRUST` · proxy impl name

### 💎 Bounty Hunter

Chain-wide scan (not wallet-specific). Manual refresh. $10+ threshold. 4 engines:

|Engine|Source         |Finds                                                           |
|------|---------------|----------------------------------------------------------------|
|1     |Pending block  |Stuck pending txs with value + underpriced gas (replaceable)    |
|2     |Last 10 blocks |Failed txs where status=0x0 but value > 0 (max 5 receipts/block)|
|3     |Known contracts|ETH balance in 20+ protocol contracts above threshold           |
|4     |Pending pool   |EIP-1559 replacement tx builder with 25% fee bump               |

SPEED UP button sends proper EIP-1559 replacement tx (maxFeePerGas + maxPriorityFeePerGas). Chains: ETH, ARB, BASE, OP, POLY, BSC, AVAX, FTM, SONIC.

### ◎ Solana

SOL balance, SPL tokens, staked SOL, recent transactions via Solscan V2 API.

### 🦊 MetaMask

Feature breakdown with cross-reference table (Sweep Engine vs MetaMask). Deep links to Buy, Earn, Swaps, Card, Perps, RWAs, Predict, SDK. Shows live scan data (ETH balance, token count, staked, NFTs).

### 🚀 Agents

GitHub token-gated auto-deploy for all 17 AGENTS.md/CLAUDE.md/skill files across 3 repos via GitHub API.

### 📡 RPC Explorer

1000+ chains from Chainlist.org. Privacy filters, TVL sort, WSS toggle, testnet toggle, USE IN SCAN override.

-----

## Supported Chains

|Chain    |Symbol|Chain ID|ERC-20        |NFTs|Bounty|
|---------|------|--------|--------------|----|------|
|Ethereum |ETH   |1       |✅             |✅   |✅     |
|BNB Chain|BNB   |56      |✅             |✅   |✅     |
|Arbitrum |ETH   |42161   |✅             |✅   |✅     |
|Polygon  |POL   |137     |✅             |✅   |✅     |
|Optimism |ETH   |10      |✅             |✅   |✅     |
|Base     |ETH   |8453    |✅             |✅   |✅     |
|Avalanche|AVAX  |43114   |✅             |✅   |✅     |
|Linea    |ETH   |59144   |✅             |✅   |—     |
|Gnosis   |xDAI  |100     |✅             |✅   |—     |
|Ink      |ETH   |57073   |✅             |✅   |—     |
|Plasma   |ETH   |1101    |✅             |✅   |—     |
|Fantom   |FTM   |250     |✅             |✅   |✅     |
|Sonic    |S     |146     |✅             |✅   |✅     |
|Aptos    |APT   |—       |🔗 Display only|—   |—     |
|Solana   |SOL   |—       |✅ Separate tab|—   |—     |

-----

## Architecture

Single-file `index.html` — all HTML, CSS, JS inline. Deployed via GitHub Pages. No Node, no npm, no build pipeline. Owner deploys from iPhone/Android via GitHub web editor. Edit → commit to main → live in ~60 seconds. **Always output the complete `index.html`.**

-----

## API Keys

|Service               |Usage                                           |
|----------------------|------------------------------------------------|
|Etherscan (shared key)|All 13 EVM chains                               |
|Solscan V2            |SOL balance, SPL tokens, staking, transactions  |
|CoinGecko (public)    |Native token + ERC-20 prices                    |
|Reservoir (public)    |NFT floor prices                                |
|OKLink                |Contract verification (user-provided at runtime)|

-----

## Skills

|Domain             |Path                              |
|-------------------|----------------------------------|
|Stack & conventions|`.agents/skills/stack/SKILL.md`   |
|Deploy workflow    |`.agents/skills/deploy/SKILL.md`  |
|Security           |`.agents/skills/security/SKILL.md`|

-----

## Version History

- **V18** — Fixed all 16 audit holes: Money Finder live, Safe Executor live, ABI/social/NFT/ERC-20 multi-chain, EIP-1559 bounty speedup, approval block range, incoming USD, Sonic address, rate limiting
- **V17** — Bounty Hunter tab (chain-wide stuck/failed/unclaimed/replacement scanning)
- **V16** — Intel Engine (6-phase auto-run: ABI, verification, approvals+revoke, internal txs, incoming transfers, social proof)
- **V15** — Fantom (FTM), Sonic (S), Aptos display card
- **V14** — OKLink Contract Verify, MetaMask tab, AGENTS.md auto-deploy
- **V13** — OKLink verify tab (standalone)
- **V12** — Money Finder, Gnosis Safe Executor, Solana, RPC Explorer, Tokens, LP, staking
- **V7** — Initial multi-chain scanner, NFTs, Sweep queue

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

### 🔴 Intel Engine

Fires automatically after every scan — zero interaction until you approve. Six sequential phases run silently in the background:

|Phase|Engine               |What it does                                                                                                                                                                                          |
|-----|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|1    |ABI Lookup           |Queries Etherscan `getsourcecode` for every unique contract. Decodes ABI, resolves contract names                                                                                                     |
|2    |Verification Status  |Flags unverified contracts with ⚠ badge in Contracts tab                                                                                                                                              |
|3    |Token Approvals      |Scans `Approval` event logs across all chains. Separates infinite (∞) from limited. One-tap REVOKE or batch REVOKE ALL                                                                                |
|4    |Internal Transactions|Pulls `txlistinternal` per chain — value moved via contract calls not visible in main tx list                                                                                                         |
|5    |Incoming ERC-20      |Catches tokens received without any outgoing tx from your wallet                                                                                                                                      |
|6    |Social Proof         |For each contract in your history: pulls recent callers → scores by overlap with your wallet fingerprint → measures success rate + value returned → detects honeypots → verifies proxy implementations|

**Social Proof Logic (Phase 6):**

- Only your contracts — wallets with zero overlap to you are ignored
- Any overlap with your contract interaction set = “similar wallet”
- Trust criteria: average success rate ≥70% across similar wallets
- Honeypot detection: sweepable contract where zero similar wallets ever received value back → flagged, never auto-queued
- Proxy check: reads EIP-1967 implementation slot, verifies implementation contract separately
- **TRUSTED** contracts: marked in Contracts tab + auto-added to sweep queue if sweepable
- Results: trust score %, similar wallet count, value-returned rate, proxy impl name

**Contracts tab badges per row:** `✓ verified` · `⚠ UNVERIFIED` · `🤝 87% TRUSTED` · `⚠ HONEYPOT` · `LOW TRUST` · proxy implementation name

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

- **V16** — Intel Engine (6-phase: ABI lookup, verification, token approvals + revoke, internal txs, incoming transfers, social proof verification with honeypot detection and proxy check)
- **V15** — Added Fantom (FTM), Sonic (S), Aptos display card
- **V14** — Added OKLink Contract Verify tab, MetaMask integration tab, AGENTS.md auto-deploy tab
- **V13** — OKLink verify tab (standalone)
- **V12** — Money Finder, Gnosis Safe Executor, Solana (Solscan V2), RPC Explorer, Tokens, LP Pools, staking detection
- **V7** — Initial multi-chain scanner, NFTs, Sweep queue
