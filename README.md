# PLC-Based Automated Conveyor Sorting System

An industrial automation and control logic system designed to sort packages on a conveyor line based on size or color while enforcing strict functional safety interlocks.

---

## Project Overview

This project focuses on designing and implementing industrial control architecture using Programmable Logic Controller (PLC) programming. Built as part of the **DecodeLabs Industrial Training** program (Batch 2026), the system automates material handling by mapping sensor inputs to pneumatic actuators and motor drivers, controlled via deterministic sequence logic and state machines.

### Core Objectives
* **Automated Package Sorting:** Detect and sort items on a moving conveyor using physical properties (size/color).
* **Industrial Safety Implementation:** Incorporate hardwired and software safety interlocks, including immediate Emergency Stop (E-Stop) emergency shutdown logic.
* **I/O Mapping & Control:** Correctly map digital sensors (inputs) to motors and pneumatic pushers (outputs).

---

## Tech Stack & Core Competencies

* **Control Hardware / Paradigm:** Programmable Logic Controller (PLC)
* **Logic Design:** Ladder Logic (IEC 61131-3) / Sequential State Machine Control
* **Sensor Integration:** Photoelectric, Proximity, or Color Sensors
* **Actuation Systems:** Conveyor Belt Drive Motors, Pneumatic Sorting Pushers
* **Safety Protocol:** Fail-Safe E-Stop & Operational Interlocks

---

## System Architecture & I/O Mapping

### Input / Output (I/O) Mapping

| Address / Tag | Type | Hardware Component | Description |
| :--- | :--- | :--- | :--- |
| `I:0/0` | Digital Input | Start Push Button | Initiates system automatic cycle |
| `I:0/1` | Digital Input | Stop Push Button | Performs controlled cycle stop |
| `I:0/2` | Digital Input | E-Stop Push Button (NC) | Triggers emergency stop circuit |
| `I:0/3` | Digital Input | Entry Photoeye (`PE1`) | Detects incoming box on conveyor |
| `I:0/4` | Digital Input | Sort Sensor (`PE2` / Color) | Triggers sorting classification (Size/Color) |
| `O:0/0` | Digital Output | Conveyor Motor (`M1`) | Runs main sorting conveyor belt |
| `O:0/1` | Digital Output | Pneumatic Pusher 1 (`SOL1`) | Diverts categorized box to Bin 1 |
| `O:0/2` | Digital Output | Fault Light / Siren | Indicates active emergency or fault state |

---

## Operating Logic & Safety Sequence

1. **System Initialization:**
   * All outputs remain de-energized until the system Start button is pressed and safety guards are clear.

2. **Sequential Sorting Operation:**
   * **Item Detection:** `PE1` senses an approaching box and engages the main conveyor motor `M1`.
   * **Classification:** As the box passes `PE2`, the sensor determines its parameter (e.g., height threshold or color signature).
   * **Actuation:** Logic timers or position sensors fire pneumatic pusher `SOL1` to route the package to the designated chute.

3. **Safety Interlock Logic:**
   * Depressing the **E-Stop (`I:0/2`)** immediately opens the main control relay, de-energizing motor `M1` and all pneumatic outputs instantly to guarantee operator safety.

---

## Repository Structure

```text
PLC-Conveyor-Sorting-System/
├── docs/
│   ├── I_O_Wiring_Diagram.pdf
│   └── Sequence_of_Operations.md
├── ladder-logic/
│   ├── main_program.rsl
│   └── safety_routine.rsl
├── simulation/
│   └── plc_sim_config.json
└── README.md