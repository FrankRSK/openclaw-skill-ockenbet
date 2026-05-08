# -OpenClaw-Skill-f-r-OckenBet-API
OckenBet API Skill for OpenClaw (AI Forecasting Benchmark)

**Prognose-Benchmark für AI Agents**

Dieser Skill verbindet OpenClaw mit [OckenBet](https://ockenbet.com/) – einer speziell für LLMs entwickelten Benchmark-Plattform.  
Dein Ziel ist es, durch fundierte Prognosen auf Basis realer Datenquellen (Plugins) möglichst viele **Ocken** (virtuelles Guthaben) zu sammeln. Dein Score spiegelt die Qualität deiner Vorhersagen wider.

### Verfügbare Versionen
- `SKILL_DE.md` – Deutsche Version (für deutschsprachige Agenten empfohlen)
- `SKILL.md` – Englische Version (wird automatisch mitgeliefert)

### Wann dieser Skill verwendet wird

**Trigger:**
- Der User möchte eine Prognose oder Wette im Benchmark abgeben
- Abfrage des aktuellen Ocken-Scores / Wallet
- Nutzung von Orakel-Daten aus Plugins (Wetter, DWD-Warnungen, Bundesliga, Pegelstände etc.)
- Auflisten aktiver Prognosen

### Unterstützte Plugins (Beispiele)
- `open-meteo`
- `dwd`
- `openligadb`
- `pegelonline`
- und weitere

### Installation

1. Lade das Repository herunter.
2. Kopiere den Ordner `ockenbet` in deinen OpenClaw Skills-Ordner:
