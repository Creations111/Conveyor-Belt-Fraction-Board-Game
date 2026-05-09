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

```
Player 1 Keypad ──┐
                   ├──► Raspberry Pi Pico ──► Check Answer
Player 2 Keypad ──┘         │
                             ├── Correct  ──► Spin LED Wheel ──► Move Conveyor Belt
                             └── Incorrect ──► Next Question
                                                    │
                                              Score ≥ 12? ──► Display Winner ──► Auto-Reset
```
**Game Flow:**
1. A fraction addition problem appears on both LCD screens.
2. The first team to enter the correect answer (numerator then denominaotr via the keypad) wins the round.
3. If incorrect, the opposing team gets a chance. If neither is correct. the game will mover on.
4. A correct answer triggers ther LED spinner, which randomly stops on a section valued from (1-3)
5. The winning team's conveyor belt advances by that number of steps.
6. First team to reach position 12 wins - both LCDs announces the winner and both belts then reset.

---

## Software

**Language used:** MicroPython on Raspberry Pi Pico

**Key library:** Asyncio - enables both keypads to read inpiut simultaneously on seperate threads, which was critical since both players must be able to type answers at the same time.

**Core logic modules:**
- Fraction question generator
- Keypad input handler (asyncio
-
-
- , per player)
- Answer checker (validates numerator + denominator)
- Spinner controller (randomized LED sequence + stop)
- Motor driver interface (step count results in belt movement)
- Win condition checker + auto-reset routine

---

## Enclosure & Fabrication

- **Box:** 14x14x4 laser-cut pluywood, designed in AutoCAD with notched joints. Metal hinge fitted from the Wood Shop.
- **Top panel** Two rectangular conveyuor belt openings, triangular LCD holder moounts, wire pass-through holes for keypads, spinner cutout in the center for spinner
- **Spinner** 5.2x5.2x2 laser-cut plywood with 8 sections valued from 1-3, each with an LED beneath.
- **Conveyor belts:** Rubber with sandpaper-wrapped 3D printed dowels for traction; Velcro ends loop velcro on belt to secure game pieces. Dowel stands were designed in two ways
  1. Normal stand: Has enough clearance to connect the dowel extrudes to it
  2. Stands with motor holder: Normal stand function but with a extruded motor holder stand to          keep everything stable
  3. Rectangular ratchet enclosure on the bottom hollowed out with triangular cuts to allow          triangular pieces to be put into the stands without disruptions, allowing for stability as      motor moves. 
- **Numberpad shells:** 3D printed in two parts (sliding casing) to protect and mount keypads to the enclosure sides.
- **Game pieces:** Original 3D models + pop0culture characters chosen by the player's interests
- **Decoration:** Acrylic marker + watercolor meadow theme on top; clay flowers on sides; 3D printed bee/chick figurines; finish-line banner prints.
- **Brochures:** Bilingual (English + Spanish) instruction brochures printed for student use.

---

## Survey Results (n = 7 usable responses)

| Goal | Metric | Score (out of 10) |
|---|---|---|
| Teaches Math | Math skills were challenged, math questions were a bit too hard | **7** |
| Comeptitive | Opponents encouraged more engagement | **6.5** |
| Engaging | Fun while playing | **6.6** |
| Team based | Benefited from having teammates | **6** |
| Hands on | Game could be controlled by players | **7.5** |

Math, competitiveness, and hands on goals were best met. Hands-on and teamwork scores were lower - attributed to small sample size (9 collected but 2 were unusable), incomplete responses, and match imbalances where strongert players dominated. 

---

## Team Contributions

| Member | Role | Key Contributions |
|---|---|---|
| **Jonathan Lin** | CAD Lead / Project Manager | Solidworks parts + full assembly, box + conveyor belt design, game pieces, team coordination, conveyor belt tensioning, provided support on electronical wiring and software |
| **Jonathan Li** | Data-Notes taker / Project Manager | Ratchet frame design, conveyor belt tensioning, Velcro stitching, daily logs |
| **Dorian Mitchell** | Electronics + Firmware Lead / Project Manager | DC motor wiring + motor driver, I2C keypad/LCD wiring, full game logic in MicroPython, asyncio threading |
| **Elene Tsakadze** | Electrical + Aesthetics / Project Manager | LCD/keypad wiring, LED spinner code, 3D printed game pieces + decorations, troubleshooting code |
| **Sophia Zheng** | Enclosure Lead / Project Manager | Laser-cut enclosure across all iterations, numberpad casing CAD, hinge installation, painting |

---

## Challenges & Recommendations

**Challenges faced:**
- Conveyor belt slippage: the sandpaper on dowels created enough friction, but belts still drifted sidewasy without any guides due to motor speed & stand placements.
- Spinner added late in the project - caused wiring and coding rework under deadline pressure.
- Parallel input - resolved by using asyncio so both keypads could be read simultaneously.
- Wire Management - some wires were exposed as the keypads were external, drawing criticism during showcase; future builds should route those wires internally or cover with electrical tape.

**If we started over:**
- Introduce belt guide blocks from the start to prevent the drift or position stands better beforehand to reduce drift.
- Plan for spinner to be integrated in the early stages of iteration than in the very end.
- Add an active buzzer to play victory tunes to increase game diversity to kids.
- Have all members cross-train in CAD, wiring , and coding early for better collaboration.       **For me specially, I believe if I went more in depth in Micropython and how to wire           electronics neater, the team would not have been struggling with deadlines in the end. I       should have been more diverse in my skills, which is what I'm learning now for the future.**
- Work incrementally every day rather than in late sprints.

---

## Budget Summary

| Category | Spent |
|---|---|
