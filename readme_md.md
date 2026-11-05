# SAP-1 Architecture Web Simulator

A lightweight, browser-based interactive simulator for the **SAP-1 (Simple-As-Possible 1)** computer architecture. The simulator provides a graphical representation of SAP-1's internal registers, 16 × 8 RAM, control logic, W-Bus data transfer, and 8-bit binary LED output.

## 🚀 How to Run

### Option 1: Live Demo (GitHub Pages)
Access the live simulator directly in your browser:
👉 [**SAP-1 Simulator Live Page**](https://veronmar.github.io/Group-8-sap1/)

### Option 2: Download & Run Locally
1. Download or clone this repository to your local computer:
   * Click the green **Code** button at the top of the GitHub repository page and select **Download ZIP**, then extract the folder.
2. Open the project folder.
3. Double-click `index.html` (or `Group-8-sap1.html`) to launch the application directly in any modern web browser.

*Note: No installation, dependencies, node packages, or build tools are required.*

---

## 🛠️ Tech Stack & Justification

* **Language / Framework:** Vanilla HTML5, CSS3, and JavaScript (Client-side only, no external frameworks).
* **Justification:** 
  - **Zero Dependency:** Built purely with native browser technologies to ensure instant execution without requiring server setups, compilers, or external package managers.
  - **Performance & Transparency:** Single-file design allows direct access to the architectural state machine and event handlers while maintaining high visual responsiveness for clock cycles and T-state transitions.

---

## 💻 Supported SAP-1 Instruction Set

| Instruction | Opcode | Function |
| :--- | :---: | :--- |
| **`LDA address`** | `0000` | Load Accumulator ($A$) from RAM memory address |
| **`ADD address`** | `0001` | Add RAM memory value to Accumulator ($A \leftarrow A + \text{RAM}$) |
| **`SUB address`** | `0010` | Subtract RAM memory value from Accumulator ($A \leftarrow A - \text{RAM}$) |
| **`OUT`** | `1110` | Output Accumulator contents to Output Register & LED Display |
| **`HLT`** | `1111` | Halt execution and stop clock signal |

---

## 🧪 Default Verification Program

The simulator includes a built-in program loader for the required formula: **$25\text{H} + 05\text{H} - 23\text{H} = 07\text{H}$**

### Memory Layout:
* `0H`: `LDA 9H` (`0000 1001`)
* `1H`: `ADD AH` (`0001 1010`)
* `2H`: `SUB BH` (`0010 1011`)
* `3H`: `OUT` (`1110 1111`)
* `4H`: `HLT` (`1111 1111`)
* `9H`: `25H` (Data operand $A$)
* `AH`: `05H` (Data operand $B$)
* `BH`: `23H` (Data operand $C$)

**Expected Output:** `07H` (Binary LEDs: `0000 0111`)