# SWEEP ENGINE V19

**Live:** https://rickybobby1236.github.io/chain-scanner

Multi-chain wallet portfolio scanner, Bitcoin intelligence engine, intel engine, bounty hunter, contract verifier, and AI agent deploy tool. Single-file architecture — no build step, no npm, no framework.

-----

## Tabs

|Tab           |Description                                                                      |
|--------------|---------------------------------------------------------------------------------|
|⚡ CONNECT     |Wallet connection — 11 wallet types + EVM paste + Solana                         |
|💰 MONEY FINDER|Live protocol scanning for unclaimed/stuck value                                 |
|🔐 SAFE EXEC   |Gnosis Safe loader, queue inspector, calldata builder, executor                  |
|🔍 SCAN        |Parallel EVM scan — 13 chains, native + tokens + LP + staking + NFTs             |
|📡 CONTRACTS   |Contract interaction history with trust badges                                   |
|🪙 TOKENS      |ERC-20 balances with USD values across all chains                                |
|💧 LIQ POOLS   |LP positions (V2 + V3) and pending rewards                                       |
|🖼 NFTs        |NFT holdings with live Reservoir floor prices — all chains                       |
|💰 SWEEP       |Full sweep queue — history + staked + LP + rewards in one batch                  |
|◎ SOLANA      |SOL balance, SPL tokens, staked SOL, tx history via Solscan V2                   |
|✅ VERIFY      |OKLink 5-endpoint contract verification                                          |
|🔴 INTEL       |6-phase auto-run: ABI, verification, approvals, internals, incoming, social proof|
|💎 BOUNTY      |Chain-wide stuck/failed/unclaimed/replacement transaction hunting                |
|🔑 BITCOIN     |Puzzle scanner, famous wallets, burned addresses, xpub/seed sweep                |
|🦊 METAMASK    |Feature breakdown, cross-reference table, deep links                             |
|🚀 AGENTS      |GitHub auto-deploy for AGENTS.md across 3 repos                                  |
|📡 RPC         |1000+ chains from Chainlist.org with privacy filters                             |

-----

## Feature Details

### ⚡ Connect

11 wallet types: MetaMask, Trust, Coinbase, Rabby, OKX, FoxWallet, Phantom, Exodus, CoinWallet, Zerion, Any injected. Paste EVM address for read-only scan. Solana supported separately via Solscan V2 API.

### 💰 Money Finder

Live protocol scanning — 11 protocols fully implemented:

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

Results ranked by USD. One-tap execute per item directly from wallet.

### 🔐 Gnosis Safe Executor

Full implementation:

- Load any Safe by address + chain via RPC
- Reads nonce, threshold, ETH balance, owner list
- Detects if connected wallet is an owner
- Loads queued txs from Safe Transaction Service API (ETH, ARB, POLY, OP, BASE)
- Click any queued tx to load into builder
- Builds full execTransaction calldata (ABI-encoded)
- Sends to wallet for signing
- Pre-loaded with nonce 137 wstETH deposit tx

### 🔍 Scan

Parallel EVM scan across 13 chains. Fetches native balances, ERC-20 tokens (all 13 chains), LP positions (Uni V2/V3, Sushi, Pancake, Camelot, Quickswap, Aerodrome), staked positions (Lido, Rocket Pool, Aave, Compound, Convex, GMX, Yearn), pending rewards, and NFTs (all chains) with Reservoir floor prices.

### ✅ Contract Verify

OKLink 5-endpoint integration: submit source, poll result, verify proxy, poll proxy result, fetch source info. Auto-fills compiler fields. Hardhat/Foundry/Truffle snippets per chain.

### 🔴 Intel Engine

Auto-runs after every scan — 6 phases, silent until complete:

|Phase|What it does                                                                                 |
|-----|---------------------------------------------------------------------------------------------|
|1    |ABI lookup + contract name resolution (all active chains)                                    |
|2    |Verification status — badge on unverified contracts                                          |
|3    |Token approvals — all chains, rolling 2yr window, one-tap REVOKE or batch REVOKE ALL INFINITE|
|4    |Internal transactions — value moved via contract calls                                       |
|5    |Incoming ERC-20 transfers with USD value                                                     |
|6    |Social proof — wallet fingerprint scoring, honeypot detection, proxy verification            |

Social Proof runs on all active chains. Pulls recent callers, scores by overlap with your contract fingerprint, measures success rate and value returned. Honeypot detection: sweepable contract + zero similar wallets received value = flagged, never auto-queued. TRUSTED contracts auto-add to sweep queue.

Contract tab badges: verified / UNVERIFIED / TRUSTED% / HONEYPOT / LOW TRUST / proxy impl name

### 💎 Bounty Hunter

Chain-wide, not wallet-specific. Manual refresh. Configurable threshold (default $10+).

|Engine|Source         |Finds                                           |
|------|---------------|------------------------------------------------|
|1     |Pending block  |Stuck pending txs + underpriced gas replacements|
|2     |Last 10 blocks |Failed txs with value > 0 (5 receipts/block max)|
|3     |Known contracts|ETH balance in 20+ protocol contracts           |
|4     |Pending pool   |EIP-1559 replacement tx builder (25% fee bump)  |

SPEED UP sends proper EIP-1559 tx (maxFeePerGas + maxPriorityFeePerGas). Chains: ETH, ARB, BASE, OP, POLY, BSC, AVAX, FTM, SONIC.

### 🔑 Bitcoin Intelligence

4 engines. API fallback: Mempool.space → Blockstream → blockchain.info.

**Puzzle #1–256**
Scans all 256 known Bitcoin puzzle addresses. Batched with rate limiting. Shows puzzle number, bit difficulty (EASY 1-20 / MEDIUM 21-50 / HARD 51-100 / EXTREME 101+), address, BTC balance, USD value.

**Famous Addresses**
16 pre-loaded: Satoshi genesis + early blocks, Hal Finney (first BTC tx), Mt. Gox cold wallet (~79,957 BTC), Silk Road seized, Bitfinex hack + DOJ recovered, PlusToken (~200k BTC), Binance cold (~248k BTC), James Howells lost HDD. Add custom addresses with labels.

**Burned / Unspendable**
8 provably unspendable: 1BitcoinEater, Genesis coinbase, Counterparty burn, Mastercoin ICO burn, OP_RETURN sink, EVM null/dead for reference. Shows BTC locked forever.

**xpub / Seed Sweep**

- xpub/ypub/zpub: Blockstream xpub API for all derived paths + balances, Mempool fallback
- BIP39 mnemonic: guides user to export xpub from wallet app (safer — seed stays on device)
- Single address: direct balance check

Runs entirely client-side. No data leaves the page.

### ◎ Solana

SOL balance, SPL tokens with USD values, staked SOL, recent transactions via Solscan V2 API.

### 🦊 MetaMask

Feature breakdown with cross-reference table. Deep links to Buy, Earn, Swaps, Card, Perps, RWAs, Prediction Markets, SDK. Shows live scan data inline.

### 🚀 Agents

GitHub token-gated auto-deploy for 17 AGENTS.md/CLAUDE.md/skill files across ScoutAI, Chain Scanner, Satoshi Puzzle Art via GitHub API.

### 📡 RPC Explorer

1000+ chains from Chainlist.org. Privacy filters (no-track/limited/tracked), TVL sort, WSS toggle, testnet toggle, USE IN SCAN RPC override.

-----

## Supported Chains

|Chain    |Symbol|Chain ID|Scan          |ERC-20|NFTs|Bounty|
|---------|------|--------|--------------|------|----|------|
|Ethereum |ETH   |1       |✅             |✅     |✅   |✅     |
|BNB Chain|BNB   |56      |✅             |✅     |✅   |✅     |
|Arbitrum |ETH   |42161   |✅             |✅     |✅   |✅     |
|Polygon  |POL   |137     |✅             |✅     |✅   |✅     |
|Optimism |ETH   |10      |✅             |✅     |✅   |✅     |
|Base     |ETH   |8453    |✅             |✅     |✅   |✅     |
|Avalanche|AVAX  |43114   |✅             |✅     |✅   |✅     |
|Linea    |ETH   |59144   |✅             |✅     |✅   |—     |
|Gnosis   |xDAI  |100     |✅             |✅     |✅   |—     |
|Ink      |ETH   |57073   |✅             |✅     |✅   |—     |
|Plasma   |ETH   |1101    |✅             |✅     |✅   |—     |
|Fantom   |FTM   |250     |✅             |✅     |✅   |✅     |
|Sonic    |S     |146     |✅             |✅     |✅   |✅     |
|Aptos    |APT   |—       |🔗 Display     |—     |—   |—     |
|Solana   |SOL   |—       |✅ Separate tab|—     |—   |—     |
|Bitcoin  |BTC   |—       |✅ Bitcoin tab |—     |—   |—     |

-----

## Architecture

Single-file `index.html` — all HTML, CSS, JS inline. GitHub Pages. No Node, no npm, no build pipeline. Deploy from iPhone/Android via GitHub web editor. Edit → commit to main → live in ~60 seconds.

**Always output the complete `index.html`. No partial diffs.**

-----

## API Keys

|Service                 |Usage                                           |
|------------------------|------------------------------------------------|
|Etherscan (shared)      |All 13 EVM chains                               |
|Solscan V2              |SOL, SPL tokens, staking, transactions          |
|CoinGecko (public)      |Token prices                                    |
|Reservoir (public)      |NFT floor prices                                |
|OKLink                  |Contract verification (user-provided at runtime)|
|Mempool.space (public)  |BTC balances, xpub, price                       |
|Blockstream (public)    |BTC balance fallback, xpub API                  |
|blockchain.info (public)|BTC balance fallback                            |

-----

## Skills

|Domain             |Path                              |
|-------------------|----------------------------------|
|Stack & conventions|`.agents/skills/stack/SKILL.md`   |
|Deploy workflow    |`.agents/skills/deploy/SKILL.md`  |
|Security           |`.agents/skills/security/SKILL.md`|

-----

## Version History

- **V19** — Bitcoin Intelligence: 256 puzzle addresses, famous wallets (Satoshi/Hal Finney/Mt.Gox/Silk Road/Bitfinex), burned addresses, xpub/seed sweep. API fallback: Mempool → Blockstream → blockchain.info
- **V18** — Fixed 16 audit holes: Money Finder live, Safe Executor live, ABI/social/NFT/ERC-20 multi-chain, EIP-1559 speedup, approval block range, incoming USD, Sonic address, rate limiting
- **V17** — Bounty Hunter: chain-wide stuck/failed/unclaimed/replacement scanning
- **V16** — Intel Engine: 6-phase auto-run with social proof and honeypot detection
- **V15** — Fantom, Sonic, Aptos display card
- **V14** — OKLink Contract Verify, MetaMask tab, AGENTS.md auto-deploy
- **V13** — OKLink verify tab
- **V12** — Money Finder, Gnosis Safe, Solana, RPC Explorer, Tokens, LP, staking
- **V7** — Initial multi-chain scanner, NFTs, Sweep queue
