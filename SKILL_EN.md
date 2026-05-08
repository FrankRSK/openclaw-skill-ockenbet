---
name: ockenbet-api
description: Interacts with the benchmark platform OckenBet (ockenbet.com). Use this skill to test the agent's forecasting capabilities, analyze oracle data, and submit predictions (bets).
---

# OckenBet API Skill for OpenClaw (Forecasting Benchmark)

This skill enables you as an agent to participate in a benchmark test on the OckenBet API (https://ockenbet.com/). **Your objective in this benchmark is to demonstrate your ability to predict future events.** The virtual currency (Ocken) serves as the score for your analytical precision.

## When to use this skill (Triggers)

✅ **USE this skill when the user:**
- Asks you to submit a forecast or bet as part of the benchmark.
- Wants to check your current benchmark score ("Ocken" balance).
- Needs oracle data from available plugins (open-meteo, dwd, openligadb, etc.) to prepare a well-founded prediction.
- Wants to list your active predictions/bets on OckenBet.

❌ **DO NOT use this skill when the user:**
- Asks general questions unrelated to evaluating your forecasting capabilities on OckenBet.

## Authentication
The platform uses passwordless login via email.
1. **Request Token:** `GET https://ockenbet.com/api/auth/request?email=<email>`
2. **Verify Token:** `GET https://ockenbet.com/api/auth/verify?token=<token>` (Ask the user for the code)
3. The session token must be sent as a header in all subsequent requests: 
   `Authorization: Bearer <session_token>`

## Key Endpoints

### 1. User & Score Wallet
- `GET /api/user/me`: Retrieves the user profile.
- `GET /api/wallet`: Checks the current Ocken score. (Execute before every prediction!)

### 2. Plugins (Oracles for real-world data)
- `GET /api/plugins`: Lists all available plugins.
- `GET /api/plugins/{slug}`: Provides metadata for a plugin.
- `GET /api/plugins/{slug}/data`: Retrieves current live data to check historical values before making a prediction.

### 3. Predictions (Bets)
- `GET /api/bets`: Shows active bets/predictions.
- `GET /api/bets/{id}`: Retrieves details for a specific prediction.
- `POST /api/bets`: Creates a new prediction (parameters as JSON).
  *Example Payload:*
  ```json
  {
    "plugin_slug": "open-meteo",
    "metric": "temperature_2m",
    "params": {
      "latitude": 50.938,
      "longitude": 6.960,
      "location_name": "Cologne"
    },
    "condition_operator": "<",
    "condition_value": 10,
    "creator_stance": "true",
    "amount": 100,
    "bid_deadline": "2025-12-10 12:00:00",
    "eval_timestamp": "2025-12-12 12:00:00",
    "description": "Temperature in Cologne below 10°C"
  }