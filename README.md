# BotBattle: UNO Edition - README

Welcome to **BotBattle: UNO Edition**, the ultimate UNO bot  challenge! In this the smartest UNO-playing bot that can beat other bots in a 4-player match.

This guide explains:
- The **card notations** used in this project
- The **rules and constraints** unique to this implementation
- **Bot implementation guidelines**
<!-- - How to **test your bot locally** -->

---

## 🃏 Card Notation
Each card is represented as a **2-character string** (sometimes 3 characters for numbers >= 10).

### ✅ Standard Cards
- **Format**: `<Color><Value>`
  - Colors: `R` = Red, `G` = Green, `B` = Blue, `Y` = Yellow
  - Values: `0-9` for number cards

### 🚨 Action Cards
- Skip: `S` (e.g., `RS` = Red Skip)
- Reverse: `R` (e.g., `GR` = Green Reverse)
- Draw Two: `P` (e.g., `YP` = Yellow Draw Two)

### 🎨 Wild Cards
- Wild: `WC` is transformed to `WR`, `WG`, `WB`, or `WY` once a color is chosen
- Wild Draw Four: `PC` becomes `PR`, `PG`, `PB`, or `PY` based on chosen color

> ⚠️ `WC` and `PC` **should never appear in play**. Bots must choose a color and return a color-coded wild like `WR` or `PR`.

---

## 🧠 Game Mechanics ( BotBattle: UNO Edition Specific)

- The game begins with **one number card** on top. Wilds or actions as the first card are redrawn.
- **Stacking is disabled**: Draw cards (like +2 or +4) cannot be stacked. When played, the next player draws and is skipped.
- **Bots cannot use `Rules.is_valid_move()`** in their logic. They must validate moves independently.
- Bots must **set the color** when playing wild or +4 cards.
- When the deck runs out, all but the last played card are reshuffled.
- The game automatically prints debug logs: draws, plays, skips, and UNO calls.

---

<!-- ## 🤖 Bot Implementation
Your bot must inherit from `BaseBot` and implement the method: -->

```python
class Player(BaseBot):
    def choose_card(self, top_card):
        # top_card: str => the current top card on the pile
        # return: str => a valid card from your hand to play, or None to draw
```

### Important Notes
- bot can access its hand via `self.hand`
- If  bot returns `None`, it draws one card. If that card is valid, it will be played automatically.
-**set the color** when playing wilds or +4s.
  - E.g., instead of `WC`, return `WR` if you want red.

---

## 🧪 Testing Your Bot Locally
Can test bot using the interactive mode in `playerBot.py`:

```bash
$ python playerBot.py
```

It will ask for the top card and your hand, then call `choose_card()` and print your move.

---
---

## 📁 Folder includes

```
- main.py               # Game engine entry point
- game_engine.py        # Core game logic
- rules.py              # Handles rule validation and card effects
- deck.py               # Initializes and reshuffles deck
- base_bot.py           # Bot base class
- playerBot.py          # bot implementation
- practice_bot.py       # Sample simple bots
```



