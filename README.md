# Fraction Frenzy — STEM Education Game

**Cornerstone of Engineering II — Northeastern University**
*Jonathan Li, Jonathan Lin, Dorian Mitchell, Elene Tsakadze, Sophia Zheng | April 2026*

<img width="1124" height="1102" alt="A6D5F5FC-4C48-4EA3-875E-30725CE127FB" src="https://github.com/user-attachments/assets/619cff47-75c3-46a4-bfbe-9435a03bf7ac" />

---

## Demonstration Video

[Presentation Video](https://youtu.be/qRW1JOPw_Ok)

---

## My Role

I served as **CAD Lead and Project Manager**, responsible for all crucial SolidWorks parts and assemblies, the box and conveyor belt design, 3D-printed game pieces, support on electrical wiring and software, and team coordination toward the final build.

---

## Overview

Fraction Frenzy is an interactive, competitive educational team game built to help 5th graders practice **fraction addition with unlike denominators**. Designed and presented at the Melrose Leadership Academy in Oakland, California, the game combines physical engineering with embedded electronics to create an engaging learning experience.

Two or more players compete head-to-head, racing to reach the finish line first by correctly solving fraction problems displayed on an LCD screen. A correct answer spins a randomized wheel, which moves the team's game piece along a conveyor belt track based on where the spin lands. The first team to reach position 12 wins.

---

## Problem Statement

Fifth graders at the Melrose Leadership Academy were identified as struggling specifically with fraction addition. Traditional instruction alone was insufficient to keep students engaged. The client requested a **team-based, competitive, hands-on** solution that could make math practice more fun and collaborative in the classroom.

---

## Solution

- Fraction problem displayed on LCD
- Player types the answer on a keypad
- A correct answer triggers the spinner
- The spinner result moves the conveyor belt

Two conveyor belts run in parallel, one per team. A central spinner with 8 LED-lit sections valued 1–3 determines how many steps the correct team advances. The game resets automatically once a winner is declared.

---

## Hardware Components

| Component | Qty | Purpose |
| --- | --- | --- |
| Raspberry Pi Pico | 1 | Main microcontroller; runs all game logic |
| 20x4 LCD with I2C adapter | 2 | Displays fraction problems and game status |
| 4x4 matrix keypad with I2C adapter | 2 | Player input for fraction answers |
| DC motor + TB6612FNG motor driver (SparkFun) | 2 | Drive the conveyor belts |
| LEDs (with 220-ohm resistors) | 8 | Illuminate spinner sections |
| Breadboards | 2 | Component wiring |
| 6x AA battery pack | 1 | Power source for motors |
| Jumper wires | Many | GPIO connections |
| Laser-cut plywood enclosure (14" x 14" x 4") | 1 | Main game board housing |
| 3D-printed parts | Several | Keypad shells, LCD holders, game pieces, spinner mounts, dowels, dowel stands |
| Velcro conveyor belts (rubber + sandpaper) | 2 | Player position tracking and movement to the end and back |
| Acrylic paint, clay, watercolor | N/A | Meadow-themed decoration |

**Total team spend: $63.67 out of pocket ($135 total component value)**

---

## How It Works

```
Player 1 Keypad ──┐
                  ├──► Raspberry Pi Pico ──► Check Answer
Player 2 Keypad ──┘         │
                            ├── Correct  ──► Spin LED Wheel ──► Move Conveyor Belt
                            └── Incorrect ──► Next Question
                                                   │
                                             Score >= 12? ──► Display Winner ──► Auto-Reset
```

**Game flow:**

1. A fraction addition problem appears on both LCD screens.
2. The first team to enter the correct answer (numerator, then denominator, via the keypad) wins the round.
3. If the answer is incorrect, the opposing team gets a chance. If neither team is correct, the game moves on to the next problem.
4. A correct answer triggers the LED spinner, which stops randomly on a section valued 1–3.
5. The winning team's conveyor belt advances by that number of steps.
6. The first team to reach position 12 wins. Both LCDs announce the winner and both belts reset.

---

## Software

**Language:** MicroPython on the Raspberry Pi Pico

**Key library:** `asyncio` — reads both keypads concurrently within a single event loop, which was critical since both players must be able to type answers at the same time.

**Core logic modules:**

- Fraction question generator
- Keypad input handler (one asynchronous task per player)
- Answer checker (validates numerator and denominator)
- Spinner controller (randomized LED sequence and stop)
- Motor driver interface (step count translates to belt movement)
- Win condition checker and auto-reset routine

---

## Enclosure & Fabrication

- **Box:** 14" x 14" x 4" laser-cut plywood, designed in AutoCAD with notched joints. Metal hinge fitted from the Wood Shop.
- **Top panel:** Two rectangular conveyor belt openings, triangular LCD holder mounts, wire pass-through holes for the keypads, and a central cutout for the spinner.
- **Spinner:** 5.2" x 5.2" x 2" laser-cut plywood with 8 sections valued 1–3, each with an LED beneath.
- **Conveyor belts:** Rubber belts running on sandpaper-wrapped 3D-printed dowels for traction; Velcro ends loop onto the belt to secure game pieces. Dowel stands were designed in three configurations:
  1. **Standard stand:** enough clearance to seat the dowel extrusions.
  2. **Stand with motor holder:** the same function as the standard stand, plus an extruded motor holder to keep the assembly stable.
  3. **Rectangular ratchet enclosure:** hollowed out on the bottom with triangular cuts so triangular pieces seat into the stands without obstruction, maintaining stability as the motor runs.
- **Keypad shells:** 3D printed in two parts (sliding casing) to protect the keypads and mount them to the enclosure sides.
- **Game pieces:** Original 3D models plus pop-culture characters chosen based on player interests.
- **Decoration:** Acrylic marker and watercolor meadow theme on top; clay flowers on the sides; 3D-printed bee and chick figurines; finish-line banner prints.
- **Brochures:** Bilingual (English and Spanish) instruction brochures printed for student use.

---

## Survey Results (n = 15 responses)

| Goal | Metric | Score (out of 10) |
| --- | --- | --- |
| Teaches math | Math skills were challenged; questions were slightly too hard | **8** |
| Competitive | Opponents encouraged more engagement | **8.5** |
| Engaging | Fun while playing | **9** |
| Team-based | Benefited from having teammates | **7** |
| Hands-on | Game could be controlled by players | **9** |

---

## Team Contributions

| Member | Role | Key contributions |
| --- | --- | --- |
| **Jonathan Lin** | CAD Lead / Project Manager | SolidWorks parts and full assembly, box and conveyor belt design, game pieces, team coordination, conveyor belt tensioning, support on electrical wiring and software |
| **Jonathan Li** | Data/Notes Taker / Project Manager | Ratchet frame design, conveyor belt tensioning, Velcro stitching, daily logs |
| **Dorian Mitchell** | Electronics + Firmware Lead / Project Manager | DC motor and motor driver wiring, I2C keypad/LCD wiring, full game logic in MicroPython, asyncio task structure |
| **Elene Tsakadze** | Electrical + Aesthetics / Project Manager | LCD and keypad wiring, LED spinner code, 3D-printed game pieces and decorations, code troubleshooting |
| **Sophia Zheng** | Enclosure Lead / Project Manager | Laser-cut enclosure across all iterations, keypad casing CAD, hinge installation, painting |

---

## Challenges & Recommendations

**Challenges faced:**

- **Conveyor belt slippage:** the sandpaper on the dowels created enough friction, but the belts still drifted sideways without guides, due to motor speed and stand placement.
- **Late spinner integration:** adding the spinner near the end of the project caused wiring and coding rework under deadline pressure.
- **Parallel input:** resolved by using `asyncio` so both keypads could be read concurrently.
- **Wire management:** some wires were left exposed because the keypads mounted externally, which drew criticism during the showcase. Future builds should route these wires internally or cover them.

**If we started over:**

- Introduce belt guide blocks from the start, or position the stands more precisely beforehand, to prevent drift.
- Plan for the spinner to be integrated in the early stages of iteration rather than at the very end.
- Add an active buzzer to play victory tunes, giving the game more variety for kids.
- Have all members cross-train in CAD, wiring, and coding early for better collaboration. **Speaking for myself, if I had gone deeper into MicroPython and learned to wire electronics more cleanly, the team would not have struggled with deadlines at the end. I should have built a broader skill set, which is what I am working on now.**
- Work incrementally each day rather than in late sprints.

---

## Budget Summary

| Category | Spent |
| --- | --- |
| Keypads (x2) | $20.00 |
| LCDs (x2) | $17.00 |
| Velcro | $8.68 |
| Rubber and sandpaper | $17.99 |
| **Total out of pocket** | **$63.67** |

All other components (Pico, motor driver, batteries, breadboards, PLA, plywood) were sourced from the Northeastern Makerspace.

---

## Acknowledgements

Built as part of **Cornerstone of Engineering II** at Northeastern University — Oakland Campus.
Presented at **Melrose Leadership Academy**, Oakland, California.
Team: **JJDES Design** — Jonathan Li, Jonathan Lin, Dorian Mitchell, Elene Tsakadze, Sophia Zheng
