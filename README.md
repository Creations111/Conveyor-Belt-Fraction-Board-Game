# Fraction Frenzy - STEM Education Game
**Cornerstone of Engineering II - Northeastern University**
*Jonathan Li, Jonathan Lin, Dorian Mitchell, Elene Tsakadze, Sophia Zheng | April 2026*

---

## Overview

Fraction Frenzy is an interactive, competitive educational team game that is built to help 5th graders practice **fraction addition with different denominators**. Designed and presented at the Melrose Leadership Academy in Oakland, California, the game combines physical engineering with embedded electronics to create an engaging learning experience. 

Two or more players go hand in hand, competiting to reach the finish line first by correctly solving fraction problems displayed on an LCD screen. Correct answers spin a randomized wheel, which would move their game piece along a conveyor belt track depending where the spin lands on. First to reach the poisiton 12 would win. 

---

## Problem Statement

Fifth graders at the Melrose Leadership Academy were identified as struggling specifically with fraction addition. It was clear that traditional instructions alone were insufficient in keeping students engaged. The client requested a **team-based, competitive, hands-on, engaging** solution that could make math practice more fun and collaborative around the classroom.

---

## Solution

> **Fraction problem on LCD
- Player types answers on keypad
- Correct answer triggers spinner
- Spinner result moves conveyor belt

Two conveyor belts run in parallel, one per team. A central spinner (with 8 LED-lit sections valued from 1-3) determiens how many steps a correct team advances. The game then resets automatically when a winner is declared. 

---

## Hardware Componenets 

| Component | Qty | Purpose |
|---|---|---|
| Raspberry Pi Pico | 1 | Main micrcontroller: it runs all game logic |
| 20x4 LCD with I2C adapter | 2 | Player input for fraction answers |
| 4x4 Matrix Keypad with I2C adapter | 2 | Player input for fraction asnwers |
| DC Motor + TB6612FNG Motor Driver from SparkFun | 2 | Drive the conveyor belts |
| LEDs (220ohm resistors) | 8 | Illuminate spinner sections |
| Breadboards | 2 | Components are wired to this |
| 6x AA Battery Pack | 1 | Power source for motors |
| Jumper Wires | Many | GPIO connections |
| Laser-cut Plywood Enclosure (14x14x4) | 1 | Main game baord housing |
| 3D Printed Parts | Several | Numberpad shells, LCD holders, game pieces, spinner mounts, dowel, dowel stands |
| Velcro Conveyor Belt (rubber + sandpaper) | 2,4 | Player point tracking and movement to end and back |
| Acrylic paint, clay, watercolor | N/A | Meadow-themed decoration |

**Total Team Spend: $64 out of pocket ($135 total value)**

---

## How It Works

