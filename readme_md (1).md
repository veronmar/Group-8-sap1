# SAP-1 Simulator - Claymorphism

A browser-based interactive visual simulator for the **SAP-1 (Simple-As-Possible 1)** computer architecture. Built with plain HTML, CSS, and JavaScript, it visually demonstrates the internal registers, 16 × 8 RAM, controller-sequencer signals, W-Bus data flow, and an 8-bit binary LED output display.

---

## 🚀 How to Run

### Option 1: Live Demo (GitHub Pages)
Access the live simulator directly in your browser:
👉 [**SAP-1 Web Simulator**](https://veronmar.github.io/Group-8-sap1/)

### Option 2: Download & Run Locally
1. Click the green **Code** button at the top right of this repository page.
2. Select **Download ZIP** and extract the files on your local machine.
3. Open the extracted folder and double-click `index.html` (or your main `.html` file) to run the simulator instantly in any modern web browser. No local web server, Node.js, or build packages are required.

---

## 🛠️ Language and Framework

- **Tech Stack:** Vanilla HTML5, CSS3, and JavaScript (Client-side only).
- **Justification:** Built without external frameworks to keep the project lightweight, dependency-free, easy to distribute via simple file download, and transparent for learning low-level computer architecture.

---

## 🧪 Step-by-Step Testing & Execution Instructions

### Scenario 1: Running the Default Formula ($25\text{H} + 05\text{H} - 23\text{H} = 07\text{H}$)

1. **Input Values:**
   - On the right panel under **Load program**, enter your custom values:
     - **A** = `25`
     - **B** = `05`
     - **C** = `23`
   - Select the desired operators (`+` and `-`).

2. **Load into RAM:**
   - Click **Build and load**.
   - Check the **RAM viewer (16 × 8)** at the bottom right. Address `0H` through `4H` will display instructions (`LDA 9`, `ADD A`, `SUB B`, `OUT`, `HLT`), and addresses `9H`, `AH`, and `BH` will store your data bytes (`25H`, `05H`, `23H`).

3. **Execute Simulation:**
   - Adjust the **Clock speed** slider (e.g., set to `1.2 Hz` or `2.0 Hz`).
   - Click **Run** to auto-execute, or click **Step** to advance by instruction, or **T-state** to advance micro-operations tick-by-tick.

4. **Verify Output:**
   - Watch the **W-Bus** animations and register updates.
   - When the program hits `HLT` (Address `4H`), the **Binary output display** will light up LEDs for `0000 0111` ($07\text{H} = 7$).

---

### Scenario 2: Changing Memory Locations & Assembly Code (e.g., moving $25\text{H}$ from `9H` to `8H`)

1. **Edit Assembly Code directly:**
   - In the **Program (address: instruction or hex byte)** text box, edit your memory mapping:
     - Change `0: LDA 9` $\rightarrow$ `0: LDA 8`
     - Change `9: 25` $\rightarrow$ `8: 25`

2. **Re-load Memory:**
   - Click **Load into RAM**.

3. **Verify Layout in RAM Viewer:**
   - Scroll down to the **RAM viewer** table. Address `8H` will now hold `25H` (data), and address `0H` will display opcode `08H` (`LDA 8H`).

4. **Run Simulation:**
   - Click **Run** to verify the simulator fetches data from location `8H` correctly during the fetch-decode-execute cycle.

---

## 💻 Supported Instruction Set

| Instruction | Opcode (Hex) | Binary Opcode | Description |
| :--- | :---: | :---: | :--- |
| **`LDA address`** | `0` | `0000` | Load Accumulator ($A$) from RAM memory location |
| **`ADD address`** | `1` | `0001` | Add RAM memory value to Accumulator ($A \leftarrow A + \text{RAM}$) |
| **`SUB address`** | `2` | `0010` | Subtract RAM memory value from Accumulator ($A \leftarrow A - \text{RAM}$) |
| **`OUT`** | `E` | `1110` | Output Accumulator value to Output Register & LED array |
| **`HLT`** | `F` | `1111` | Stop execution and halt clock ticks |
