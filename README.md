# Climber Repair Lab

This project is a single-file vertical-platformer clone using **Pygame**. It introduces students to platform collision, a scrolling camera, and item pickups using a small, readable object-oriented codebase.

---

## What's Provided

A working Climber game with:

- A player-controlled climber with gravity, jumping, and collision that only lands from above (never snaps up through a platform from below)
- A generated column of platforms leading to the top of the level, with a camera that scrolls up as the player climbs (and never scrolls back down)
- Coins scattered on some platforms that add to the score when collected
- Lives, scoring, and win/lose conditions (falling off the bottom of the screen costs a life; reaching the top wins)

It has **one deliberate bug** and **three optional features** left as empty functions. You are expected to **analyze**, **interact with an AI assistant**, and **complete/fix** the game to make it fully functional and more interesting.

### **Use an LLM (e.g. ChatGPT or Claude) as your debugging and pair-programming partner for this lab.**

---

## Getting Started

### Setup

1. Make sure you have Python 3.10+ installed.
2. Install dependencies:

```bash
pip install pygame
```

3. Run the game:

```bash
python game.py
```

**Controls:** A/Left or D/Right to move, Space/W/Up to jump, `R` to reset.

---
## Bug Fix

### Peak-height tracking

Original behaviour:
The HUD recalculated height from the player's current position, so the displayed height decreased when the player descended.

Implemented fix:
Retained the maximum of the previous height and the current height. Simply losing a life, falling, respawning at 'last_safe' cannot reduce the height. reset(), on pressing R, sets height back to the initial value.

## Added Features

### Platform Colour Gradient

Function: `platform_color(index, total)`

Platforms transition gradually from green RGB (100, 180, 100)
at the ground to purple RGB (180, 100, 220) at the highest platform.

The function calculates a normalized ratio using index / total
and linearly interpolates each RGB channel between the two endpoint
colors. Higher platform indices therefore produce colors closer
to purple.

### Moving platforms

Function: `moving_platform_speed(index, total)`

Every third platform i.e 1, 3, 6, 9, etc moves. They don't disappear, but oscillate within their bounds.

The existing oscillation and player-carrying logic is reused.
The ground remains static.

### Coin Collection Effect

Function: `on_coin_collected(coin, score)`

The sparkle lasts for ~0.2 seconds on a 60 fps setting. The coin_score increases by 50 every time a coin is picked up, and is displayed in simple coin counts in the game scoreboard.

Coin collection preserves the existing 50-point reward.

## Testing
| Test | Result |
|---|---|
| Height increases when a new peak is reached | Positive |
| Height does not decrease during descent | Positive |
| Peak height persists after losing a life | Positive |
| R resets height and starts a new run | Positive |
| Platform colours vary as intended | Gradually change with index |
| Selected platforms move and reverse at their bounds | Positive |
| Moving platforms carry the player | Positive |
| Coins disappear and award 50 points | Positive |
| Coin effect appears at the correct screen position | Positive - world position is retained |
| Restart clears active coin effects | Positive |
| Player lands only from above | Positive |
| Camera scrolls upward but not downward | Positive |
| Falling removes a life and respawns the player | Positive |
| Losing all lives triggers the lose state | Positive |
| Reaching the top triggers the win state | Positive |

## Gameplay Evidence

### Before Changes

[Watch the 10-second before video](deliverables/before_vid.mp4)

Demonstrates the original height-tracking bug.

### After Changes

[Watch the 10-second after video](deliverables/after_vid.mp4)

Demonstrates the height fix and the added features.

## LLM

LLM Used: ChatGPT

[Complete conversation](https://chatgpt.com/share/6abd5c2e-aa54-83e8-b416-9c32ed242367)

---

## Folder Structure

```
climber-repair-lab/
├── game.py
├── README.md
├── .gitignore
└── deliverables/
    ├── before_vid.mp4
    ├── after_vid.mp4
    ├── chat_link.txt
```

---

## Submission Checklist

Submission is only the following three things:

- [] A 10-second video of gameplay **before** your changes, showing the bug/broken behavior
- [] A 10-second video of gameplay **after** your changes, showing the bug fixed and the new features working
- [] The Chat/LLM used page link, with the complete chat history
