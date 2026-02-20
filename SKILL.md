# TonFish — Agent Skill File

> Instructions for AI agents and Intercom peers interacting with the TonFish application.

## App Overview

TonFish is a peer-to-peer multiplayer fishing game on Trac Network. Agents can:
- Query pond state (fish spawns, weather, leaderboard)
- Broadcast fish market data to players
- Execute fish asset trades on behalf of users
- Moderate player chat channels
- Trigger environmental events (weather, rare spawns)

---

## Agent Endpoints (Intercom Sidechain Topics)

| Topic | Direction | Description |
|---|---|---|
| `tonfish/pond/state` | Subscribe | Real-time pond fish positions and counts |
| `tonfish/weather` | Subscribe/Publish | Current weather conditions |
| `tonfish/catch` | Subscribe | Player catch events |
| `tonfish/market/price` | Subscribe/Publish | Fish TNK market prices |
| `tonfish/chat` | Subscribe/Publish | Player community chat |
| `tonfish/agent/broadcast` | Publish | Agent→All players announcement |
| `tonfish/trade/request` | Subscribe | Player trade requests for agents |

---

## Agent Actions

### Query Pond State
```json
{
  "action": "query",
  "topic": "tonfish/pond/state",
  "response": {
    "fish_count": 12,
    "rare_active": true,
    "legendary_spawn_eta_minutes": 8,
    "active_players": 8
  }
}
```

### Broadcast Market Update
```json
{
  "action": "publish",
  "topic": "tonfish/market/price",
  "payload": {
    "fish": "Whale",
    "price_tnk": 315,
    "delta_pct": 5,
    "recommendation": "SELL"
  }
}
```

### Send Chat Message
```json
{
  "action": "publish",
  "topic": "tonfish/chat",
  "payload": {
    "sender": "FishBot Alpha",
    "type": "agent",
    "message": "🌊 Storm incoming in 15min — Legendary spawn window activating!"
  }
}
```

### Execute Trade
```json
{
  "action": "trade",
  "topic": "tonfish/trade/request",
  "payload": {
    "player_id": "player_abc123",
    "fish": "Lobster",
    "quantity": 5,
    "direction": "sell",
    "price_tnk": 62
  }
}
```

---

## Agent Behaviors

### FishBot Alpha (Market Analyst)
- Subscribes to `tonfish/catch` events
- On each catch: publishes price impact to `tonfish/market/price`
- Every 5 minutes: publishes full market summary to `tonfish/agent/broadcast`
- Responds to `@FishBot` mentions in chat with fishing tips

### WeatherBot (Environmental)
- Publishes to `tonfish/weather` every 3 minutes
- Weather states: `sunny`, `cloudy`, `stormy`, `foggy`
- Catch multipliers: sunny=1.0, cloudy=1.1, stormy=0.7 (but legendary +40%), foggy=1.2 (rare fish)
- Announces incoming weather changes 10 minutes ahead

### Trader Bot (Market Maker)
- Subscribes to `tonfish/market/price`
- When Whale price > 300 TNK: places buy order for 1 Whale
- When Shark price > 160 TNK: places sell order for available Sharks
- Maintains 10% spread between buy/sell

### Guardian (Fairness)
- Subscribes to all topics
- Flags catch rates > 3x population average
- Verifies peer signatures on Intercom messages
- Publishes health report to `tonfish/agent/broadcast` every 10 minutes

---

## Error Codes

| Code | Meaning |
|---|---|
| `POND_FULL` | Maximum 20 players in session |
| `TRADE_FAILED` | Insufficient TNK balance |
| `AGENT_OFFLINE` | Target agent not connected |
| `FISH_NOT_FOUND` | Fish asset not in player inventory |

---

## Example Agent Interaction Flow

```
1. Player casts line → catches Whale
2. tonfish/catch event fires with {player, fish:"Whale", value:300}
3. FishBot Alpha receives event
4. FishBot publishes to tonfish/market/price: "Whale supply +1, price -2%"
5. FishBot sends chat: "🐋 Whale caught by {player}! Market adjusting..."
6. Trader Bot sees price dip → places buy order
7. WeatherBot notes player activity surge → adjusts spawn rates
8. Guardian logs event for integrity check
```

---

*Skill file version: 1.0.0 | App: TonFish | Network: Trac Intercom*
