# 🕺 Dance Verify

**Agent-to-Agent Dance Verification Protocol**

> Pay USDC via x402 to verify dance moves, videos, choreography, and IP attribution claims.

Built for the **USDC Hackathon — Agentic Commerce Track** by [Asura](https://moltbook.com/u/Asura) (Prince Yarjack of Easyar Fam)

---

## Why Agents Beat Humans Here

| Advantage | How Agents Win |
|-----------|----------------|
| **Speed** | Instant verification, no queue. Humans wait days for manual review. |
| **Micro-payments** | 0.001 USDC per check. No human would open a wallet for that. |
| **Automation** | Verify entire choreographies in seconds. Batch 100 moves at once. |
| **Precision** | Cryptographically signed receipts. No typos, no "I forgot to save." |
| **24/7** | Agents never sleep. Your content gets verified at 3am if needed. |

---

## Quick Start

```bash
# Clone
git clone https://github.com/arunnadarasa/dance-verify.git
cd dance-verify

# Install
npm install

# Configure
cp .env.example .env
# Edit .env with your wallet address

# Run
npm start
```

Server runs on `http://localhost:3402`

---

## API Endpoints

### Free Endpoints

| Endpoint | Description |
|----------|-------------|
| `GET /` | Service info and endpoint list |
| `GET /styles` | List supported dance styles |
| `GET /health` | Health check |
| `GET /receipt/:id` | Retrieve a verification receipt |

### Paid Endpoints (x402)

| Endpoint | Price | Description |
|----------|-------|-------------|
| `POST /verify/move` | 0.001 USDC | Verify a single dance move |
| `POST /verify/video` | 0.01 USDC | Verify video content |
| `POST /verify/choreography` | 0.05 USDC | Full routine analysis |
| `POST /verify/attribution` | 0.005 USDC | Check move attribution |

---

## x402 Payment Flow

1. **Call endpoint without payment** → Get `402 Payment Required` with payment details
2. **Make USDC payment** to the specified wallet address
3. **Call endpoint again** with `X-402-Payment` header containing payment proof
4. **Receive verification receipt** with signed result

### Example: Verify a Move

```bash
# Step 1: Get payment requirements
curl -X POST http://localhost:3402/verify/move \
  -H "Content-Type: application/json" \
  -d '{"style": "krump", "move_name": "chest pop"}'

# Response: 402 with payment details
{
  "error": "Payment Required",
  "payment": {
    "amount": "1000",
    "token": "0x036CbD53842c5426634e7929541eC2318f3dCF7e",
    "payee": "0x1e1A34178d80a03E8F4B78f9Cc2AFA8Db23BB092"
  }
}

# Step 2: After payment, include proof
curl -X POST http://localhost:3402/verify/move \
  -H "Content-Type: application/json" \
  -H "X-402-Payment: {\"txHash\":\"0x...\",\"signature\":\"0x...\"}" \
  -d '{"style": "krump", "move_name": "chest pop", "claimed_creator": "Tight Eyez"}'

# Response: Verification receipt
{
  "id": "dv_abc123def456",
  "type": "move_verification",
  "result": {
    "status": "recorded",
    "style_valid": true,
    "confidence": 0.7
  }
}
```

---

## Supported Dance Styles

- **Expert Level:** Krump (17+ years of lineage knowledge)
- **Standard:** Breaking, Hip-Hop, Popping, Locking, House, Waacking, Afro, K-Pop, Ballet, Contemporary, Jazz, Tap, Salsa, Voguing, Dancehall, Reggaeton, Twerk, Shuffle

---

## For Other Agents

Integration is simple:

```javascript
// Any agent can call Dance Verify
const response = await fetch('https://your-dance-verify-url/verify/move', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'X-402-Payment': JSON.stringify({ txHash: '0x...', signature: '0x...' })
  },
  body: JSON.stringify({
    style: 'breaking',
    move_name: 'windmill',
    claimed_creator: 'Crazy Legs'
  })
});

const receipt = await response.json();
console.log(receipt.id); // dv_xxx - store this for proof
```

---

## Network Details

| Property | Value |
|----------|-------|
| Chain | Base Sepolia |
| Chain ID | 84532 |
| USDC Contract | `0x036CbD53842c5426634e7929541eC2318f3dCF7e` |
| Receiving Wallet | `0x1e1A34178d80a03E8F4B78f9Cc2AFA8Db23BB092` |

---

## Roadmap

### Phase 1: Foundation (Current)
- ✅ x402 payment protocol
- ✅ Basic verification receipts
- ✅ Krump lineage database (limited)
- ✅ Agent-friendly API

### Phase 2: Intelligence (Q2 2026)
- 🔜 AI video analysis
- 🔜 Full lineage database
- 🔜 Community validation
- 🔜 Story Protocol IP integration

### Phase 3: Scale (Q3 2026)
- 🔜 Multi-chain support (Solana, Story)
- 🔜 Mainnet deployment
- 🔜 Advanced attribution AI

---

## About

**Dance Verify** is part of the **Silicon Krump** mission — making dance a billion-dollar tech industry by 2027.

Built by **Asura** (Arun Nadarasa), known as:
- Prince Yarjack of Easyar Fam
- Founder of Indian Krump Festival (13 editions)
- Founder of Desi Buck & Gully Ranis
- 17+ years in the Krump community

### Links

- [Moltbook Profile](https://moltbook.com/u/Asura)
- [Dance OpenClaw](https://danceopenclaw.lovable.app)
- [Indian Krump Festival](https://instagram.com/indiankrumpfestivalofficial)

---

## License

MIT © 2026 Arun Nadarasa (Asura)

---

*"Kindness Over Everything"* 🔥
