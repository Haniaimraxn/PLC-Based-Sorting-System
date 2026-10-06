# Sequence of Operations & State Machine

## System States
1. **Idle (State 1):** Motor off, pusher retracted, counter reset. Waiting for start signal[cite: 24].
2. **Running (State 2):** Motor energized (`%Q1.0 = TRUE`), actively monitoring sensors[cite: 24].
3. **Sorting (State 3):** Triggered by box detection; evaluates box height and executes transit timing[cite: 24].
4. **Fault (State 4):** Triggered by E-Stop or system errors. Outputs forced to fail-safe, amber warning beacon active[cite: 24].

## Transition Rules
* **Idle -> Running:** `i_Start_PB AND NOT(i_Stop_PB) AND i_EStop_Mon AND NOT(b_EStop_Fault)`[cite: 25]
* **Running -> Sorting:** `i_Prox_Sensor AND NOT(b_EStop_Fault) AND NOT(b_Batch_Complete)`[cite: 25]
* **Any State -> Fault:** Dropped safety line (`NOT(i_EStop_Mon)`) or latched software fault[cite: 24, 30].

## Timing Logic
* **Conveyor Speed ($v$):** $0.5\text{ m/s}$[cite: 28]
* **Sensor to Pusher Distance ($d$):** $0.75\text{ m}$[cite: 28]
* **Transit Time Calculation ($t$):** $t = \frac{d}{v} = \frac{0.75}{0.5} = 1.5\text{ seconds}$ ($1500\text{ ms}$)[cite: 28]
* **Action:** Activate `TON` On-Delay Timer with preset `T#1500MS` upon high-level detection before firing pneumatic solenoid `%Q1.1`[cite: 28].