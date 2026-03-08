# DecentAI Protocol — Full Implementation

> **The first decentralised AI inference marketplace on Arc chain.**
> Pay per token in USDC. No subscription. No lock-in. On-chain settlement.

---

## Repository Layout

```
decentai-full/
├── contracts/          # Solidity smart contracts (Hardhat project)
│   ├── contracts/
│   │   ├── DecentAIInference.sol   # Billing + USDC settlement
│   │   └── ModelRegistry.sol       # On-chain model catalog + node bids
│   ├── scripts/
│   │   ├── deploy.js               # Deploy DecentAIInference
│   │   ├── deploy_registry.js      # Deploy ModelRegistry
│   │   ├── create-wallet.js        # Generate a fresh deployer wallet
│   │   └── verify.js               # Verify deployed contract state
│   ├── test/
│   │   ├── DecentAIInference.test.js
│   │   └── ModelRegistry.test.js
│   ├── hardhat.config.js
│   └── package.json
│
├── router/             # Python inference router (FastAPI)
│   ├── main.py                 # App entry point, all HTTP endpoints
│   ├── contract.py             # Web3.py wrapper for DecentAIInference
│   ├── model_registry.py       # Syncs ModelRegistry from chain
│   ├── node_registry.py        # Node health + latency tracking
│   ├── billing_queue.py        # Async retry queue for failed charges
│   ├── pricing.py              # Fee calculation engine
│   ├── models.py               # Static model definitions + metadata
│   ├── metrics.py              # Prometheus-style counters
│   ├── rate_limiter.py         # Per-wallet rate limiting
│   ├── openai_fallback.py      # GPT-4o / Claude proxy node
│   ├── demo.py                 # CLI demo script
│   └── requirements.txt
│
├── frontend/           # Static HTML dashboards
│   ├── index.html              # Landing page (hybridy.site)
│   └── dashboard.html          # User dashboard (deposit/balance/history)
│
├── docs/               # Full documentation
│   ├── architecture.md
│   ├── contracts.md
│   ├── router.md
│   ├── deployment.md
│   ├── api-reference.md
│   └── node-operator.md
│
├── scripts/            # Operational helper scripts
│   ├── setup.sh                # One-command environment setup
│   ├── health-check.sh         # Verify all services are running
│   └── smoke-test.sh           # End-to-end inference call test
│
└── .env.example        # All environment variables documented
```

## Quick Start

```bash
# 1. Clone / unzip
cd decentai-full

# 2. Run setup
chmod +x scripts/setup.sh && ./scripts/setup.sh

# 3. Fill in .env
cp .env.example .env
# edit .env — at minimum: DEPLOYER_PRIVATE_KEY, CONTRACT_ADDRESS

# 4. Deploy contracts
cd contracts && npm install && npm run deploy

# 5. Start router
cd ../router && pip install -r requirements.txt
uvicorn main:app --reload --port 8000

# 6. Verify
../scripts/health-check.sh
```

## Network

| Parameter | Value |
|-----------|-------|
| Chain | Arc Testnet |
| Chain ID | `5042002` |
| RPC | `https://rpc.testnet.arc.network` |
| Explorer | `https://explorer.testnet.arc.network` |
| Settlement | USDC (native Arc token) |
| Fee model | 10% protocol / 90% node |

## Contact

hello@hybridy.site · hybridy.site
