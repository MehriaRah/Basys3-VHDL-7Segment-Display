# Basys3-VHDL-7Segment-Display
A VHDL implementation of a 4-digit 7-segment display controller using a Finite State Machine (FSM) on the Basys 3 FPGA board.

# FPGA-Based 4-Digit 7-Segment Display Controller
**Hardware:** Xilinx Artix-7 (Basys 3 Development Board)  
**Language:** VHDL  
**Toolchain:** Xilinx Vivado Design Suite  

## 🎯 Project Overview
This project implements a robust hardware controller for a multiplexed 4-digit 7-segment display on a Basys 3 FPGA. The design focuses on efficient resource utilization, precise timing control, and hardware-level safety constraints.

### Core Engineering Competencies:
* **Synchronous Digital Design:** Implementation of a 3-process FSM architecture.
* **Hardware Efficiency:** Optimized Hex-to-7-Segment encoding via minimized lookup tables.
* **Timing Analysis:** Full verification of setup/hold times and critical path delays at 100 MHz.

## ⚙️ System Logic & Design Methodology
The design follows industry-standard VHDL practices to ensure reliability and scalability.

### 1. Synchronous FSM & Timing Control
The core of the system is a **3-process Finite State Machine (FSM)**:
* **Sync Process:** Manages the 30-bit internal counter and state registers on the rising edge of the 100 MHz clock.
* **Delta Process (Next-State Logic):** Computes the next state based on current counter values and real-time switch inputs. 
* **Lambda Process (Output Logic):** Maps states to physical LED patterns for the display.

### 2. High-Speed Multiplexing & Digit Selection
Since the 4-digit display shares common segment lines, the design uses a multiplexing scheme to drive the digits sequentially:
* **One-Hot Encoding:** Activates a single digit at a time via low-active enable lines (AN0-AN3).
* **Persistence of Vision:** By utilizing the high-order bits of a 30-bit counter, the refresh rate is optimized to eliminate flicker while maintaining a clear, readable display for the human eye.

### 3. Dynamic Range & Input Validation
A key feature is the integration of user-defined counting ranges:
* **Input Sanitization:** The logic monitors 4-bit slide switch inputs (SW). 
* **Hardwired Safety:** To prevent invalid display states, the VHDL code includes a conditional check: if the user input exceeds decimal `9`, the system automatically defaults to a maximum value of `9`.
* **Synchronous Reset:** The counter resets immediately upon reaching the validated maximum value, ensuring a clean decimal loop.

## 📈 Engineering Performance Analysis
To ensure hardware reliability, a post-implementation timing analysis was conducted using the Vivado Timing Engine:
* **Critical Path:** Identified in the 30-bit adder logic.
* **Performance:** The design successfully met all timing constraints for the 10 ns (100 MHz) clock period.
* **Reliability:** The implementation maintains a significant slack margin, ensuring stable operation across varying environmental conditions.

## 🚀 How to Run
1. Open Xilinx Vivado and import the source files from the `src/` directory.
2. Add the `.xdc` constraints file to map the VHDL signals to the Basys 3 physical pins.
3. Run **Synthesis** and **Implementation**.
4. Generate the **Bitstream** and program the Artix-7 FPGA.

📸 Hardware Validation: Initial Digit Encoding
The image below demonstrates the successful hardware implementation of the first project milestone: Static 7-Segment Digit Encoding.

Logic Verification: The Artix-7 FPGA is successfully driving the seven-segment display using low-active VHDL logic.

Segment Mapping: The segment pattern for the decimal value "4" is active, confirming that the VHDL lookup table (LUT) and pin assignments in the .xdc file are correctly mapping bitstreams to the physical LEDs.

Digit Selection: The left-most anode (AN3) is enabled via a one-hot encoded signal, while the remaining three anodes are held high (disabled) to prevent ghosting.

<img width="940" height="750" alt="lab 3 first task" src="https://github.com/user-attachments/assets/1511f757-be1a-4b79-89ab-5365691c8bd9" />




