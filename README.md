<div align="center">

<img src="https://blindwoods.app/icon.png" alt="Blindwoods" width="96" />

# Blindwoods

### We can't see you.

**A private AI on Robinhood Chain where paying and asking never meet.**

[![Chain](https://img.shields.io/badge/Robinhood%20Chain-4663-1E3A2F)](https://blindwoods.app/docs)
[![Ticker](https://img.shields.io/badge/ticker-%24BLIND-E8A33D?labelColor=1E3A2F)](#holder-allowance)
[![Ticket](https://img.shields.io/badge/ticket-%240.01-F3F1EA?labelColor=1E3A2F)](#tickets)
[![Contracts](https://img.shields.io/badge/contracts-ownerless-F3F1EA?labelColor=1E3A2F)](#money-nobody-can-redirect)
[![Third parties](https://img.shields.io/badge/third--party%20scripts-0-1E3A2F)](#nothing-watches-the-chat)

[Website](https://blindwoods.app) · [App](https://app.blindwoods.app) · [Docs](https://blindwoods.app/docs) · [X @blindwoodsRH](https://x.com/blindwoodsRH)

</div>

---

## About

Every private AI on a public chain asks you to connect a wallet. That wallet becomes your account, and on a public chain your account is a public portfolio: every coin you hold, every trade you made. Every question you ask gets filed next to it.

Blindwoods splits the two with blind signatures. Your wallet buys tickets. The tickets ask the questions. The server can check that a ticket was paid for, but it cannot tell which wallet paid, because it signed that ticket without being able to read it.

There is no account to watch. $BLIND holders get fresh tickets every day, paid for by trading fees.

> *Blind*: the tickets are signed blind, and the server is blind to who is asking. *Woods*: where nobody follows you.

---

## Features

### Two doors, one wall

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
```

The page that asks questions loads no wallet code at all. The page that handles the wallet never sees a question.

### Blind tickets

| Feature | Detail |
|---|---|
| **Blind signing** | Your device blinds each ticket; the issuer signs without seeing it (blind RSA, RFC 9474, as Privacy Pass tokens) |
| **Batch draws** | Up to **200** tickets per draw |
| **Daily keys** | One issuer key per UTC day; a ticket lives **72 hours**, then its key and spent list are deleted |
| **Kept on your device** | Tickets live in your browser, with no wallet field |
| **Move between devices** | Export tickets as one line of text and import them on a phone or into an agent |

### Tickets

| Tickets in a pack | Price (USDG) |
|---|---|
| 500 | $5 |
| 2,500 | $25 |
| 10,000 | $100 |
| 50,000 | $500 |

One price: **$0.01 a ticket** = one standard private message. A long conversation costs one more ticket per 2,000 tokens, never more than 8 on one request. Tickets the gate did not spend come back to you.

### Verified in your browser

Before the first question, your browser runs five checks on the enclave:

| Check | Passes when |
|---|---|
| Published release | The enclave's code release is fetched with its digest |
| Signed and logged code | The release is signed by its build and recorded in a public transparency log |
| Hardware report | The report is signed by the processor vendor's keys |
| Measurements match | What the hardware measured equals what the release declares |
| Key bound to the enclave | The key your question is encrypted to is named inside that report |

A failed or missing check is a failure, never a warning. Nothing is sent until all five pass.

### Nothing watches the chat

- Your question is **encrypted to the enclave** before it leaves your device; the gate only passes ciphertext along
- The gate keeps **no request log, no body, no address**
- **Zero third-party scripts**, locked by the page's Content-Security-Policy
- Conversation history stays **in your browser**: export it or wipe it anytime
- No email, no username, no avatar: there is no "you" on any screen

### Holder allowance

Holding $BLIND never buys privacy: a claimed ticket and a bought ticket are the same object. Holding buys **free tickets every day**.

| Tier | Hold | Free tickets a day | Unlocks |
|---|---|---|---|
| Wanderer | 0 | 0 | Packs at $0.01, standard models, full privacy |
| Sapling | 100,000 $BLIND | up to 20 | Gift seeds |
| Grove | 1,000,000 $BLIND | up to 250 | Premium models (3 tickets a message) |
| Old Growth | 10,000,000 $BLIND | up to 3,000 | Pictures, API tickets for agents, a model vote |

Balances are checked now and at two random blocks in the last 24 hours. Caps are super-linear, so splitting a bag across wallets never earns more.

### Money nobody can redirect

Five contracts on Robinhood Chain, none with an owner, none pausable or upgradeable.

| Contract | Does |
|---|---|
| **TicketMint** | Sells packs and splits every purchase in the same call: 80% operations, 10% Compute Pool, 10% buyback and burn |
| **FeeRouter** | Launches $BLIND on Pons (USDG pair, 1% creator tax) and splits the fee 50% Compute Pool, 20% buyback and burn, 20% builders, 10% Leak Bounty |
| **ComputePool** | Pays for holders' daily tickets, to one fixed payee, at most 1/30 of the pool per day |
| **BuybackBurner** | Buys $BLIND and sends every token to the dead address |
| **BountyVault** | Pays leak reports on two of three judges' approval |

```
$BLIND trade ─► 1% creator tax ─► FeeRouter ─► 50% Compute Pool ─► holders' daily tickets
                                           ├─► 20% buyback and burn
                                           ├─► 20% builders
                                           └─► 10% Leak Bounty Vault
```

### Leak Bounty

| Finding | Share of the vault |
|---|---|
| Link a ticket to a wallet | 50% |
| Find a stored prompt or answer | 30% |
| Catch a third-party script or call | 10% |
| Any other privacy defect | 5% |

### The meter

A public page shows hourly totals and contract balances, each linked to its source on chain: tickets spent, burns, the bounty vault, and the count that matters most, **tickets that named a wallet: 0**.

### For agents

The same gate serves scripts and agents: tickets in the `Authorization: PrivateToken` header, the familiar chat-completions body, no API key and no account.

### On the way

| Phase | Adds |
|---|---|
| 2 | Oblivious HTTP relay (the gate never sees an IP), pictures, seed links, the Forest, agent quick start |
| 3 | Own enclave nodes, reproducible builds, zero-knowledge holding proofs, split issuer key |
| 4 | Partner apps that accept tickets, self-funding agents, a mobile app |

---

<div align="center">
<sub>Blindwoods is a community project, not affiliated with Robinhood Markets, any brokerage, the launchpad, any model provider or any hardware vendor. Nothing here is investment advice. $BLIND gives access to tickets and features inside the product, nothing more, and can lose all of its value. There is no presale and the team never DMs first; the contract address appears on blindwoods.app and @blindwoodsRH only. Blind tickets cannot protect what you type, your device, or a network you do not control.</sub>
</div>
