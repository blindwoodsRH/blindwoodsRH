<div align="center">

<img src="https://blindwoods.app/icon.png" alt="Blindwoods" width="96" />

# Blindwoods

### We can't see you.

**A private AI on Robinhood Chain where paying and asking never meet.**
Your wallet buys blind-signed tickets. Each ticket asks one question of a model inside a hardware enclave.
The server can check that a ticket was paid for. It cannot tell which wallet paid.

[![Chain](https://img.shields.io/badge/Robinhood%20Chain-4663-1E3A2F)](https://blindwoods.app/docs)
[![Ticker](https://img.shields.io/badge/ticker-%24BLIND-E8A33D?labelColor=1E3A2F)](#token-at-a-glance)
[![Ticket](https://img.shields.io/badge/ticket-%240.01-F3F1EA?labelColor=1E3A2F)](#highlights)
[![Contracts](https://img.shields.io/badge/contracts-ownerless-F3F1EA?labelColor=1E3A2F)](documents/blindwoods-kernel)
[![Third parties](https://img.shields.io/badge/third--party%20scripts-0-1E3A2F)](documents/blindwoods-cabin)

[Website](https://blindwoods.app) · [App](https://app.blindwoods.app) · [Docs](https://blindwoods.app/docs) · [X @blindwoodsRH](https://x.com/blindwoodsRH) · [GitHub](https://github.com/blindwoodsRH)

</div>

---

## What is Blindwoods

Every private AI on a public chain asks you to connect a wallet, and that wallet becomes your account: a public portfolio filed next to every question you ask. Blindwoods splits the two with blind signatures. Your wallet pays at one door; a ticket asks at another; nothing the service runs can join them. $BLIND holders receive fresh tickets every day, paid for by a fixed share of trading fees.

- **Pay with a wallet, ask with a ticket.** Blind RSA (RFC 9474) as Privacy Pass tokens: the issuer never sees the ticket it signed.
- **Nothing to log.** No accounts, no questions on disk, no column that ties a ticket to a wallet.
- **Verified by you.** Five enclave checks run in your browser before anything is sent.
- **Zero third-party code** on the chat page, locked by its Content-Security-Policy.
- **Money with no owner.** Five contracts split every dollar on fixed terms nobody can change.
- **A price on breaking it.** The Leak Bounty pays up to half its vault for a ticket linked to a wallet.

## Highlights

| Mechanic | Value |
|---|---|
| Ticket price | **$0.01** = one standard private message (1,000 tokens out) |
| Packs (USDG) | 500 · 2,500 · 10,000 · 50,000 tickets |
| Ticket life | 72 hours after its key; one issuer key per UTC day |
| Draw size | Up to 200 blind tickets per draw |
| Per request | 1 to 8 tickets; +1 per 2,000 tokens of conversation |
| Pack split | 80% operations · 10% Compute Pool · 10% buyback and burn |
| Creator fee split | 50% Compute Pool · 20% buyback and burn · 20% builders · 10% Leak Bounty |
| Enclave checks | Release digest · signed and logged code · hardware report · measurements · bound key |
| Leak Bounty | 50% link · 30% stored prompt · 10% third-party call · 5% other |

## How It Works

```
   DOOR 1 · THE WALLET                          DOOR 2 · THE TICKET
 ┌──────────────────────────┐   ##   ┌──────────────────────────────┐
 │ pay USDG for a pack,     │   ##   │ hand over 1 ticket + a       │
 │ or prove you hold $BLIND │   ##   │ question sealed to the       │
 │                          │   ##   │ enclave                      │
 │ server sees:             │   ##   │ server sees:                 │
 │ "wallet X is owed N"     │   ##   │ "a valid, unspent ticket"    │
 └────────────┬─────────────┘   ##   └──────────────┬───────────────┘
              │ N signatures, made blind            │ enclave answers,
              ▼                                     ▼ nothing stored
      N tickets live on YOUR device ───────► spent one at a time

            ## = the wall: no field, log or key crosses it

   EVERY TRADE BUYS A PROMPT
   $BLIND trade ─► 1% creator tax ─► FeeRouter ─► 50% Compute Pool ─► holders' daily tickets
                                              ├─► 20% buyback and burn
                                              ├─► 20% builders
                                              └─► 10% Leak Bounty Vault
```

## Repository Layout

| Repository | What it contains |
|---|---|
| [**blindwoods-kernel**](documents/blindwoods-kernel) | `TicketMint` reference contract with Foundry tests, interfaces for `FeeRouter`, `ComputePool`, `BuybackBurner` and `BountyVault`, and the C4 container model in `SYSTEM_DESIGN.md` |
| [**blindwoods-canon**](documents/blindwoods-canon) | `THESIS.md`, the full argument from the account problem to the ownerless contracts, and `THREAT_MODEL.md`, a STRIDE model with Web3 abuse patterns and the leak reporting process |
| [**blindwoods-harness**](documents/blindwoods-harness) | `@blindwoods/harness`, a TypeScript SDK for agents that pay per call in tickets, plus `ENDPOINTS.md` covering every route and status code |
| [**blindwoods-cabin**](documents/blindwoods-cabin) | The Next.js app shell: chat screen, IndexedDB ticket store, enclave check, strict CSP |

### Marketing collateral

Outside this folder, in the project workspace:

| Folder | Contents |
|---|---|
| `Caption/` | `CAPTION.md` (29 long-form captions) and `CAPTION-SHORT.md` (30 operator-log posts) |
| `Article/` | `X-Article.md` (3 X Articles) |

## Holder Tiers

| Tier | Hold | Free tickets a day | Unlocks |
|---|---|---|---|
| Wanderer | 0 | 0 | Packs at $0.01, standard models, full privacy |
| Sapling | 100,000 $BLIND | up to 20 | Gift seeds |
| Grove | 1,000,000 $BLIND | up to 250 | Premium models (3 tickets a message) |
| Old Growth | 10,000,000 $BLIND | up to 3,000 | Pictures, API tickets for agents, a model vote |

Holding never buys privacy: a claimed ticket and a bought ticket are the same object. Balances are checked now and at two random blocks in the last 24 hours, and caps are super-linear, so splitting a bag never pays.

## Token at a Glance

| | |
|---|---|
| Ticker | **$BLIND** |
| Chain | Robinhood Chain (chainId 4663) |
| Launchpad | Pons, fair launch, USDG pair |
| Supply | 1,000,000,000, fixed, no mint function |
| Team allocation | None. No presale, no private round |
| Dev buy | At most 2%, inside the launch transaction, 90-day linear vesting |
| Creator tax | 1% on every trade, routed by the ownerless FeeRouter |
| Contract address | Published on [blindwoods.app](https://blindwoods.app) and pinned on X at launch. Not before. |

## Tech Stack

| Layer | Technology |
|---|---|
| Contracts | Solidity 0.8.28, Foundry, Robinhood Chain |
| Tickets | Privacy Pass type 2, blind RSA (RFC 9474, 9577, 9578) |
| App | Next.js 16, React 19, viem, IndexedDB |
| Issuer and gate | Node 22 route handlers, OpenSSL via `node:crypto`, AES-256-GCM wrapped keys |
| Inference | Open-weight models in attested CPU and GPU enclaves, requests sealed with HPKE |
| Ledger | Postgres with forced row-level security and a dedicated least-privilege role |
| Runtime | Non-root containers (uid 1001), no published ports, TLS reverse proxy |

## Roadmap

| Phase | Window | Ships |
|---|---|---|
| **1 · MVP** | days 1 to 10 | Ownerless contracts, issuer, gate, standard enclave model, browser attestation, USDG packs, meter, launch receipt |
| **2 · Growth** | weeks 2 to 6 | Oblivious HTTP relay, pictures, seed links, the Forest, live Leak Bounty, agent API quick start |
| **3 · Upgrade** | months 2 to 4 | Own enclave nodes, reproducible builds, zero-knowledge holding proofs, split issuer key |
| **4 · Ecosystem** | months 4 to 12 | Partner apps accept tickets, self-funding agents, mobile app, models by holder vote |

## Quick Start

Each part lives in its own repository.

```bash
# contracts
git clone https://github.com/blindwoodsRH/blindwoods-kernel.git
cd blindwoods-kernel/contracts && forge install foundry-rs/forge-std --no-git && forge test && cd ../..

# agent SDK
git clone https://github.com/blindwoodsRH/blindwoods-harness.git
cd blindwoods-harness && npm install && BLINDWOODS_TICKETS='bwt1.…' npm run example && cd ..

# app
git clone https://github.com/blindwoodsRH/blindwoods-cabin.git
cd blindwoods-cabin && npm install && npm run dev
```

The thesis and threat model: [github.com/blindwoodsRH/blindwoods-canon](https://github.com/blindwoodsRH/blindwoods-canon).

## ⚠️ Scam Warning

- **$BLIND has not launched until the official account says so.** Any token using the name before then is not ours.
- **There is no presale, no private round, no whitelist and no allocation.** Anyone offering one is a scammer.
- **The team will never DM you first.** Anything a stranger sends you about Blindwoods is a scam.
- **Blindwoods never asks for a seed phrase or a private key.** Signing in is a message signature with no transaction.
- **Trust only the official channels:** [blindwoods.app](https://blindwoods.app), [app.blindwoods.app](https://app.blindwoods.app), [@blindwoodsRH](https://x.com/blindwoodsRH) and [github.com/blindwoodsRH](https://github.com/blindwoodsRH). The contract address appears there and nowhere else first.

## Reference Links

| Resource | Link |
|---|---|
| Website, meter, launch receipt | [blindwoods.app](https://blindwoods.app) |
| App | [app.blindwoods.app](https://app.blindwoods.app) |
| Docs and threat model | [blindwoods.app/docs](https://blindwoods.app/docs) |
| X | [@blindwoodsRH](https://x.com/blindwoodsRH) |
| GitHub | [github.com/blindwoodsRH](https://github.com/blindwoodsRH) |
| RFC 9474, blind RSA | [rfc-editor.org/rfc/rfc9474](https://www.rfc-editor.org/rfc/rfc9474) |
| RFC 9577, Privacy Pass HTTP auth | [rfc-editor.org/rfc/rfc9577](https://www.rfc-editor.org/rfc/rfc9577) |
| RFC 9578, Privacy Pass issuance | [rfc-editor.org/rfc/rfc9578](https://www.rfc-editor.org/rfc/rfc9578) |

---

<div align="center">
<sub>Blindwoods is a community project. It is not affiliated with Robinhood Markets, any brokerage, the launchpad, any model provider or any hardware vendor. Nothing here is investment advice. $BLIND gives access to tickets and features inside the product, nothing more, and can lose all of its value. Blind tickets protect the link between a payment and a question; they cannot protect what you type, your device, or a network you do not control.</sub>
</div>
