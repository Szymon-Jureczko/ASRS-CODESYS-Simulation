# Automated Storage and Retrieval System (ASRS) Simulation

A complete PLC program and HMI visualization for an automated warehouse crane, built entirely in CODESYS using Structured Text (ST). 

This project simulates a smart 2-axis gripper system that automatically sorts and stores incoming items into a dynamically managed 5x5 grid warehouse. It was designed to showca!
se high-performance logic-to-HMI synchronization, decoupled task management, and closed-loop motion simulation.
[2026-02-23 19-20-47(1)](https://github.com/user-attachments/assets/ae5a648d-2d01-412e-b2a6-270b34c084e0)
## Key Features

* **Proportional Motion Control (P-Control):** Replaced basic linear movement with an exponential "ease-out" algorithm `(Current := Current + (Target - Current) * 0.2)`. This allows the crane to move at high velocities while landing smoothly, eliminating visual jitter and simulating real-world physical inertia.
* **Decoupled Task Architecture:** Optimized CPU load by separating the physics/math calculations (`MainTask` at 20ms) from the UI rendering (`VISU_TASK` at 50ms) while utilizing client-side animation interpolation.
* **Robust State Machine Design:** The core logic is driven by an ST `CASE` statement, handling complex sequences (Search -> Move -> Drop -> Return) safely and predictably.
* **Dynamic Data Management:** Utilizes multidimensional arrays `arrWarehouse[1..5, 1..5]` to track real-time bin capacities, item counts, and color-coded UI updates.
* **Custom HMI Interface:** Features interactive controls, live coordinate tracking, and visual safety interlocks (e.g., automated error clearing via `TON` timers).

## Tech Stack & Tools

* **Environment:** CODESYS V3.5
* **Languages:** IEC 61131-3 Structured Text (ST)
* **Visualization:** CODESYS WebVisu (Client-Side Animation Enabled)
* **Concepts:** Finite State Machines (FSM), P-Control, Task Scheduling, Array Manipulation.

## How to Run the Simulation

1. Clone this repository and open the `.project` file in CODESYS.
2. Ensure your local gateway is running (`CODESYS Control Win V3 x64`).
3. Double click the Device in the tree and hit **Scan Network** to connect.
4. Go to **Online -> Login**, then **Online -> Reset Cold** (to initialize array capacities).
5. Press **Start (F5)**.
6. Open the `TargetVisu` tab or navigate to `http://localhost:8080/webvisu.htm` to interact with the HMI.

## Author
Szymon Jureczko
