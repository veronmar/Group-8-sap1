# SAP-1 Simulator - Claymorphism

A browser-based visual simulator for the SAP-1 (Simple-As-Possible 1) computer architecture. Built with plain HTML, CSS, and JavaScript, it visually demonstrates the internal registers, 16 × 8 RAM, controller-sequencer signals, W-Bus data flow, and an 8-bit binary LED output display.

How to Run

1. Download the file.
2. Download live server extension in vscode.
3. Open the file or double-click index.html to run the simulator instantly in any modern web browser.

Language and Framework

Tech Stack:HTML, CSS, and JavaScript.
Built without external frameworks to keep the project lightweight, dependency-free, easy to distribute via simple file download, and transparent for learning low-level computer architecture.

Step-by-Step Testing & Execution Instructions

Scenario 1: Running the Default Formula (25H + 05H - 23H)

1. Input Values:
   - On the right panel under, enter your custom values:
     - A = `25`
     - B = `05`
     - C = `23`
   - Select the desired operators (`+` and `-`).

2. Load into RAM:
   - Click Build and load.
   - Check the RAM viewer (16 × 8) at the bottom right. will display instructions (`LDA 9`, `ADD A`, `SUB B`, `OUT`, `HLT`), and addresses `9H`, `AH`, and `BH` will store your data bytes (`25H`, `05H`, `23H`).
   - If you change your data starting address in the instruction text (for example, changing `LDA 9` to `LDA 8`), make sure to also update the corresponding data address label in the RAM       section below (moving your data byte from `9:` to `8:`). Then click into RAM
   - Ensure that your jump/load operand matches the exact hexadecimal memory address where your data is stored.

3. Execute Simulation:
   - Adjust the Clock speed slider.
   - Click Run to auto-execute, or click Step to advance by instruction, or T-state to advance micro-operations.

4. Verify Output:
   - Watch the W-Bus animations and register updates.
   - When the program hits `HLT` (Address `4H`), the Binary output display will light up LEDs for `0000 0111` 07H.

Supported Instruction Set

| Instruction | Opcode (Hex) | Binary Opcode | Description |
| :--- | :---: | :---: | :--- |
| **`LDA address`** | `0` | `0000` | Load Accumulator ($A$) from RAM memory location |
| **`ADD address`** | `1` | `0001` | Add RAM memory value to Accumulator ($A \leftarrow A + \text{RAM}$) |
| **`SUB address`** | `2` | `0010` | Subtract RAM memory value from Accumulator ($A \leftarrow A - \text{RAM}$) |
| **`OUT`** | `E` | `1110` | Output Accumulator value to Output Register & LED array |
| **`HLT`** | `F` | `1111` | Stop execution and halt clock ticks |
