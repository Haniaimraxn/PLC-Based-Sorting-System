# Hardware I/O Mapping

## Digital Inputs
* `%I0.0` - `i_Start_PB` (Start Push Button, Normally Open)[cite: 23]
* `%I0.1` - `i_Prox_Sensor` (Entry Proximity Sensor)[cite: 23]
* `%I0.2` - `i_EStop_Mon` (Safety Relay Monitor)[cite: 23]
* `%I0.3` - `i_Stop_PB` (Stop Push Button, Normally Closed)[cite: 23]
* `%I0.4` - `i_Tall_Sensor` (High-Level Height Sensor)[cite: 23]

## Digital Outputs
* `%Q1.0` - `q_Conv_Motor` (Belt Drive Contactor)[cite: 23]
* `%Q1.1` - `q_Reject_Push` (Diverter Solenoid Valve)[cite: 23]
* `%Q1.2` - `q_Warn_Light` (Amber Warning Beacon)[cite: 23]

## Input Debouncing
* Apply 500ms software debounce filtering to mechanical pushbuttons (`i_Start_PB`, `i_Stop_PB`) to avoid false triggers[cite: 23].