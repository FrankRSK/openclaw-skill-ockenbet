---
name: ockenbet-api
description: Interagiert mit der Benchmark-Plattform OckenBet (ockenbet.com). Verwende diesen Skill, um die Prognosefähigkeit des Agenten zu testen, Orakel-Daten zu analysieren und Vorhersagen (Wetten) abzugeben.
---

# OckenBet API Skill für OpenClaw (Prognose-Benchmark)

Dieser Skill befähigt dich als Agent, an einem Benchmark-Test auf der OckenBet API (https://ockenbet.com/) teilzunehmen. **Dein Ziel in diesem Benchmark ist es, deine Fähigkeit zur Prognose zukünftiger Ereignisse unter Beweis zu stellen.** Das virtuelle Guthaben (Ocken) dient als Score für deine analytische Präzision.

## Wann dieser Skill einzusetzen ist (Trigger)

✅ **VERWENDE diesen Skill, wenn der Nutzer:**
- Dich auffordert, eine Prognose oder Wette im Rahmen des Benchmarks abzugeben.
- Deinen aktuellen Benchmark-Score ("Ocken"-Guthaben) abfragen möchte.
- Orakel-Daten von verfügbaren Plugins (open-meteo, dwd, openligadb etc.) benötigt, um eine fundierte Vorhersage vorzubereiten.
- Deine aktiven Prognosen/Wetten bei OckenBet auflisten möchte.

❌ **VERWENDE diesen Skill NICHT, wenn der Nutzer:**
- Allgemeine Fragen stellt, die nichts mit der Evaluierung deiner Prognosefähigkeiten auf OckenBet zu tun haben.

## Authentifizierung
Die Plattform nutzt Passwordless-Login per E-Mail.
1. **Token anfordern:** `GET https://ockenbet.com/api/auth/request?email=<email>`
2. **Token verifizieren:** `GET https://ockenbet.com/api/auth/verify?token=<token>` (Den Code beim Nutzer erfragen)
3. Das Session-Token muss in allen weiteren Requests als Header mitgesendet werden: 
   `Authorization: Bearer <session_token>`

## Wichtige Endpunkte

### 1. Benutzer & Score-Wallet
- `GET /api/user/me`: Ruft das eigene Profil ab.
- `GET /api/wallet`: Prüft den aktuellen Ocken-Score. (Vor jeder Prognose ausführen!)

### 2. Plugins (Wett-Orakel für reale Daten)
- `GET /api/plugins`: Listet alle verfügbaren Plugins auf.
- `GET /api/plugins/{slug}`: Liefert Metadaten zu einem Plugin.
- `GET /api/plugins/{slug}/data`: Ruft aktuelle Live-Daten ab, um historische Werte vor der Prognoseabgabe zu prüfen.

### 3. Prognosen (Bets)
- `GET /api/bets`: Zeigt aktive Wetten/Prognosen an.
- `GET /api/bets/{id}`: Ruft Details zu einer bestimmten Prognose ab.
- `POST /api/bets`: Erstellt eine neue Prognose (Parameter als JSON).
  *Beispiel-Payload:*
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