# Restaurant Billing System

![Platform](https://img.shields.io/badge/Platform-x86%20DOS-blue)
![Language](https://img.shields.io/badge/Language-x86%20Assembly-lightgrey)
![License](https://img.shields.io/badge/License-MIT-yellow)

A 16-bit x86 DOS console application written in Assembly that presents a restaurant menu, accepts a food item and quantity from the user, and prints the total bill — all via DOS interrupt calls.

## Table of Contents

- [Features](#features)
- [How It Works](#how-it-works)
- [Toolchain](#toolchain)
- [Prerequisites](#prerequisites)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Limitations](#limitations)
- [License](#license)

## Features

- Three menu categories: Breakfast, Veg Lunch/Dinner, Non-Veg Lunch/Dinner
- Single-item ordering with quantity input and total price calculation
- Star-bordered ASCII UI rendered entirely via DOS INT 21H
- Input validation with invalid-entry detection and retry loop

## How It Works

1. The main menu presents three category choices (Breakfast / Veg / Non-Veg).
2. The selected sub-menu lists up to nine items with prices.
3. The user enters the item number and a quantity (single digit, 1–9).
4. The program multiplies quantity by the item's unit (price ÷ 10) using `MUL`, then calls `AAM` (ASCII Adjust after Multiply) to split the result into individual decimal digits, appending a literal `'0'` to reconstruct the full price (since all prices are multiples of 10).
5. The total is printed as `XXX/-` and the user can return to the main menu or exit.

## Toolchain

| Tool | Purpose |
|------|---------|
| MASM 6.x or TASM (Turbo Assembler) | Assemble `.asm` → `.obj` |
| LINK.EXE (MASM) or TLINK (TASM) | Link `.obj` → `.exe` |
| MS-DOS or DOSBox | Run the 16-bit `.exe` |

The easiest all-in-one option on modern hardware is **emu8086** (Windows), which includes an assembler, linker, and emulator in a single IDE.

## Prerequisites

- **DOSBox** (cross-platform) + TASM or MASM, **or**
- **emu8086** IDE (Windows)

## Usage

**With TASM + DOSBox:**

```dos
tasm restaurant_billing_system.asm
tlink restaurant_billing_system.obj
restaurant_billing_system.exe
```

**With MASM:**

```dos
masm restaurant_billing_system.asm;
link restaurant_billing_system.obj;
restaurant_billing_system.exe
```

**With emu8086:**

1. Open `restaurant_billing_system.asm` in emu8086.
2. Click **Compile** then **Run**.

## Project Structure

```
restaurant-billing-system/
├── restaurant_billing_system.asm   # x86 Assembly source
├── LICENSE
└── README.md
```

## Limitations

- **16-bit DOS only** — uses `.MODEL LARGE` and DOS INT 21H; will not run natively on 64-bit Windows, Linux, or macOS without a DOS emulator (DOSBox/emu8086).
- **Single-item orders only** — the billing loop handles one item per session; there is no running total across multiple items.
- **Single-digit quantity** — quantity input is read as one character (1–9); quantities of 10 or more are not supported.
- **No tax or discount logic** — prices are fixed as listed in the menu strings.

## License

Released under the [MIT License](LICENSE).
