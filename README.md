# SAP-1 Simulator

A browser-based visual simulator for the SAP-1 (Simple-As-Possible 1) computer architecture. Built with plain HTML, CSS, and JavaScript, it visually demonstrates the internal registers, 16 × 8 RAM, controller-sequencer signals, W-Bus data flow, and an 8-bit binary LED output display.

# How to Run
1. Download the file.
2. Double-click `Group8-sap1.html` to open it in any modern web browser.

No server, extensions, Node.js, or installation is needed.

# Language and Framework

**Tech stack:** HTML, CSS, and JavaScript (no framework).

**Justification:** Built without external frameworks to keep the project lightweight, dependency-free, easy to distribute through a simple file download, and transparent for learning low-level computer architecture.

# What the Interface Shows

- **Register panels:** PC, MAR, IR, Accumulator, B register, Output register, and the adder/subtractor, each with live binary and hex values.
- **RAM viewer:** a table of all 16 addresses (0H to FH) with their contents. The address currently selected by MAR is highlighted.
- **W-Bus:** lights up and animates when data moves, and shows the value on the bus and which components send and receive it.
- **Controller-sequencer:** shows the current T-state (T1 to T6) and the active control signals.
- **Binary output display:** 8 LEDs showing the Output register in binary.
- **Controls:** Build and load, Load into RAM, Step, T-state, Run, Reset, and a clock speed slider.

# Step-by-Step Testing & Execution Instructions

## Running a Formula

1. **Enter values.** Under **Load program**, type your hex values in **A**, **B**, and **C**, and choose the operators (`+` or `-`) between them. For the default formula, use A = `25`, B = `05`, C = `23` with `+` then `-`.

2. **Load into RAM.** Click **Build and load**. In the **RAM viewer**, addresses `0H` to `4H` will show the instructions (`LDA 9`, `ADD A`, `SUB B`, `OUT`, `HLT`), and addresses `9H`, `AH`, and `BH` will hold your data bytes (`25H`, `05H`, `23H`). The expected result is shown under the formula inputs.

3. **Execute.** Adjust the **Clock speed** slider, then:
   - Click **Run** to execute automatically (the button changes to **Pause**).
   - Click **Step** to execute one full instruction.
   - Click **T-state** to advance one clock tick at a time.

4. **Verify the output.** Watch the W-Bus and the register updates. When the `OUT` instruction (address `3H`) executes, the **Binary output display** lights the LEDs for the result. For the default formula this is `0000 0111` (07H = 7). The `HLT` instruction at `4H` then stops the clock.

## Sample Formulas

| Formula | Enter | Expected result | LEDs (binary) |
| :--- | :--- | :---: | :---: |
| 25H + 05H - 23H | A=`25` `+` B=`05` `-` C=`23` | `07H` | `0000 0111` |
| 10H - 05H + 20H | A=`10` `-` B=`05` `+` C=`20` | `2BH` | `0010 1011` |
| 7FH + 01H + 01H | A=`7F` `+` B=`01` `+` C=`01` | `81H` | `1000 0001` |

## Editing the Program Manually

1. In the **Program** text box, edit the assembly lines. For example, to move the first data byte from `9H` to `8H`, change `0: LDA 9` to `0: LDA 8` and change `9: 25` to `8: 25`.
2. Click **Load into RAM**. Do not click **Build and load** afterwards, because it regenerates the program text and overwrites your edits.
3. Make sure the operand of each `LDA`, `ADD`, and `SUB` matches the address where its data is stored.
4. Click **Run** or **Step** to execute.

## Reset and Clear RAM

- **Reset** clears all registers and the execution log, but keeps the program in RAM so it can be run again.
- **Clear RAM** empties all 16 memory locations.

# Supported Instruction Set

| Instruction | Opcode (Hex) | Binary Opcode | Description |
| :--- | :---: | :---: | :--- |
| **`LDA address`** | `0` | `0000` | Load Accumulator (A) from the RAM location |
| **`ADD address`** | `1` | `0001` | Add the RAM value to the Accumulator (A ← A + RAM) |
| **`SUB address`** | `2` | `0010` | Subtract the RAM value from the Accumulator (A ← A − RAM), using 2's complement |
| **`OUT`** | `E` | `1110` | Output the Accumulator value to the Output register and LED display |
| **`HLT`** | `F` | `1111` | Stop execution and halt the clock |
