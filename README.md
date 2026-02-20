# 🎣 TonFish — P2P Fishing Game on Trac Network
READY GO TO FISHERMAN TON-TRAC-FHISING
> A multiplayer peer-to-peer fishing game powered by **Trac Network's Intercom** stack, where fish are tokens, weather is shared state, and AI agents compete alongside human players.

[![Demo](https://img.shields.io/badge/Demo-Live-00d4ff?style=for-the-badge)](./index.html)
[![Fork of](https://img.shields.io/badge/Fork%20of-Trac--Systems%2Fintercom-0d2240?style=for-the-badge)](https://github.com/Trac-Systems/intercom)
[![TNK Rewards](https://img.shields.io/badge/TNK-Rewards%20Enabled-f5c518?style=for-the-badge)](#)

---

<img width="1265" height="815" alt="image" src="https://github.com/user-attachments/assets/8acfdaf4-5509-4055-a61f-47a603db61d0" />
<img width="1252" height="823" alt="image" src="https://github.com/user-attachments/assets/09ef731c-0e96-477b-bb58-41b529e7cde7" />


## 🎮 What is TonFish?

TonFish is a **real-time multiplayer fishing game** where:

- Players cast lines in a **shared virtual pond** — game state is broadcast via Intercom P2P sidechannels (no central server needed)
- **Fish are on-chain assets** redeemable for TNK via the Trac replicated-state layer
- **AI fishing agents** roam the pond autonomously: they tip players, trade fish on the market, and communicate via Intercom as first-class network participants
- **Weather conditions** (affecting fish spawn rates) are consensus state shared across all peers
- Players can **chat in real-time** via Intercom sidechannels with AI agents moderating and advising

---

## 🚀 How to Run

```bash
# Clone this repo (fork of intercom)
git clone https://github.com/YOUR_USERNAME/TonFish
cd TonFish

# Install dependencies
npm install

# Start the Intercom node + game server
npm start

# Open the game UI
open index.html
```

Or just open `index.html` directly in a browser for the UI demo.

---

## 🏗️ Architecture

```
Player Browser
   └── index.html (Game UI)
         ├── Canvas Fishing Game (client-side)
         ├── Intercom P2P Client (sidechannels)
         │     ├── Fish spawn broadcasts
         │     ├── Weather state sync
         │     ├── Player chat messages
         │     └── AI Agent communications
         └── Trac State Layer
               ├── Fish NFT ownership
               ├── TNK balance tracking
               └── Leaderboard consensus
```

### Intercom Integration Points

| Feature | Intercom Layer Used |
|---|---|
| Fish spawn events | Sidechain broadcast |
| Weather conditions | Replicated state |
| Player chat | P2P sidechain |
| AI agent tips | Agent-to-agent + agent-to-human |
| TNK transactions | Trac replicated state |
| Leaderboard | Consensus state |

---

## 🤖 AI Agents

TonFish runs **4 autonomous AI agents** over Intercom:

| Agent | Role |
|---|---|
| **FishBot Alpha** | Market analyst — tracks fish prices, recommends catches |
| **WeatherBot** | Broadcasts real-time pond conditions to all peers |
| **Trader Bot** | Automated TNK market maker — buys/sells fish assets |
| **Guardian** | Anti-cheat fairness enforcement agent |

Agents communicate with players AND each other via Intercom sidechannels. They are full peers on the network.

---

## 🐟 Fish Rarities & TNK Values

| Fish | Rarity | Base Value |
|---|---|---|
| 🦐 Shrimp | Common | 5 TNK |
| 🐠 Goldfish | Common | 10 TNK |
| 🦀 Crab | Common | 35 TNK |
| 🦞 Lobster | Rare | 60 TNK |
| 🐟 Tropical | Rare | 40 TNK |
| 🦑 Squid | Rare | 45 TNK |
| 🦈 Shark | Epic | 150 TNK |
| 🐋 Whale | Legendary | 300 TNK |

---

## 🎯 Proof It Works

- [x] Open `index.html` → fishing game loads with animated ocean
- [x] Click canvas or "CAST LINE" → fish gets caught with animation
- [x] AI agent responds to catch in Community chat
- [x] Leaderboard shows global TNK rankings
- [x] AI Agent console shows live Intercom P2P activity logs
- [x] Chat with other players + ask AI via `@FishBot` command

---

## 📄 Skills File (for AI Agents)

See [`SKILL.md`](./SKILL.md) — instructions for agents interacting with TonFish over Intercom.

---

## 💰 TRAC Reward Address

```
trac1dtlp63mkjt7kw5vyw3nxgt4sxhg7rzcn5as70t8txsvnh9l8hwmsgq9ns9
```
> ⚠️ **Replace this with your actual TRAC address before submitting!**

---

## 📚 About

- **Fork of:** [Trac-Systems/intercom](https://github.com/Trac-Systems/intercom)
- **License:** MIT
- **Built for:** awesome-intercom community payout — [Trac-Systems/awesome-intercom](https://github.com/Trac-Systems/awesome-intercom)

---

*Built with ❤️ on Trac Network. Fish responsibly.*
