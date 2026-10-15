# 🏭 OptiSort PLC: Automated Conveyor Sorting System

An industrial automation and control logic system designed to sort packages on a conveyor line based on size or color while enforcing strict functional safety interlocks.

--- 

## 📌 Description

This repository contains the complete industrial control architecture for an automated conveyor sorting line built using Programmable Logic Controllers (PLCs). Built as part of the **DecodeLabs Industrial Training** program (Batch 2026), the system automates material handling by mapping digital sensor inputs to pneumatic actuators and motor drivers through deterministic sequence logic and state machines.

The control system processes incoming packages on a moving belt, evaluates physical characteristics (package size or color signature) using digital sensors, and triggers pneumatic sorting pushers to divert items into designated bins. Beyond basic material handling, the logic implements hardwired and soft safety interlocks, status monitoring, and immediate Emergency Stop (E-Stop) shutdown routines to protect human operators and equipment.

---

## 🎯 Core Objectives
* **📦 Automated Package Sorting:** Detect and sort items on a moving conveyor using physical properties (size/color).
* **🛡️ Industrial Safety Implementation:** Incorporate hardwired and software safety interlocks, including immediate Emergency Stop (E-Stop) shutdown logic.
* **🔌 I/O Mapping & Control:** Correctly map digital sensors (inputs) to motors and pneumatic pushers (outputs).

---

## 🛠️ Tech Stack & Core Competencies

* **🎮 Control Hardware / Paradigm:** Programmable Logic Controller (PLC) / Rockwell Automation Allen-Bradley Studio 5000 / RSLogix 500
* **🧩 Logic Design:** Ladder Logic (IEC 61131-3) / Sequential State Machine Control
* **👁️ Sensor Integration:** Photoelectric, Proximity, or Color Sensors
* **⚙️ Actuation Systems:** Conveyor Belt Drive Motors, Pneumatic Sorting Pushers
* **🚨 Safety Protocol:** Fail-Safe E-Stop & Operational Interlocks

---

## 🗂️ System Architecture & I/O Mapping

### 📊 Input / Output (I/O) Mapping Table

| Address / Tag | Type | Hardware Component | Description |
| :--- | :--- | :--- | :--- |
| `I:0/0` | 🟢 Digital Input | Start Push Button | Initiates system automatic cycle |
| `I:0/1` | 🔴 Digital Input | Stop Push Button | Performs controlled cycle stop |
| `I:0/2` | 🚨 Digital Input | E-Stop Push Button (NC) | Triggers emergency stop circuit |
| `I:0/3` | 📡 Digital Input | Entry Photoeye (`PE1`) | Detects incoming box on conveyor |
| `I:0/4` | 🔍 Digital Input | Sort Sensor (`PE2` / Color) | Triggers sorting classification (Size/Color) |
| `O:0/0` | ⚙️ Digital Output | Conveyor Motor (`M1`) | Runs main sorting conveyor belt |
| `O:0/1` | 💨 Digital Output | Pneumatic Pusher 1 (`SOL1`) | Diverts categorized box to Bin 1 |
| `O:0/2` | 🚨 Digital Output | Fault Light / Siren | Indicates active emergency or fault state |

---

## ⚙️ Operating Logic & Safety Sequence

1. **🔄 System Initialization:**
   * All outputs remain de-energized until the system **Start** button (`I:0/0`) is pressed and all safety guard interlocks report clear.

2. **📦 Sequential Sorting Operation:**
   * **Item Detection:** `PE1` (`I:0/3`) senses an approaching package and energizes main conveyor motor `M1` (`O:0/0`).
   * **Classification:** As the package passes `PE2` (`I:0/4`), the sensor evaluates its target physical threshold (height or color).
   * **Actuation:** Logic timers or position pulse registers fire pneumatic pusher `SOL1` (`O:0/1`) to route the package to the designated chute.

3. **🛑 Safety Interlock Logic:**
   * Depressing **E-Stop (`I:0/2`)** immediately opens the main safety circuit, instantly de-energizing motor `M1` and pneumatic pushers to prevent damage or injury.

---

## 🚀 How to Run & Simulate

Follow these steps to set up the software environment, load the ladder logic files, and execute the conveyor simulation.

### 📋 Prerequisites
* **PLC Emulator/IDE:** RSLogix 500 / Studio 5000 Logix Designer or OpenPLC Editor.
* **Simulator (Optional):** LogixPro 500 Simulator / Factory I/O (Conveyor Sorting Scene).
* **Git:** Required to clone the repository.

---

### Step 1: Clone the Repository
Open your terminal or command prompt and run:
```bash
git clone [https://github.com/Haniaimraxn/PLC-Conveyor-Sorting-System.git](https://github.com/Haniaimraxn/PLC-Conveyor-Sorting-System.git)
cd PLC-Conveyor-Sorting-System

### Step 1: Clone the Repository
Open your terminal or command prompt and run:
