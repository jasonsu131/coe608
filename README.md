# COE608 – RISC CPU Design Project (Final Lab)

## Overview
This project is the final laboratory project for **COE608: Computer Organization and Architecture**.  
It integrates six incremental labs into the complete design, simulation, and FPGA implementation of a **RISC-style CPU** using **VHDL**.

The CPU follows a modular datapath and control unit design, emphasizing instruction execution, register transfer operations, memory access, and control logic typical of modern RISC architectures.

## Project Objectives
- Design and implement a custom RISC CPU using VHDL  
- Apply instruction set architecture (ISA) concepts  
- Build and integrate datapath and control unit components  
- Simulate and verify CPU behavior at each stage  
- Deploy and test the design on an FPGA development board  

## Tools & Technologies
- VHDL  
- Intel Quartus Prime (Quartus-II)  
- ModelSim / Quartus Simulator  
- Altera Cyclone IV FPGA  

## CPU Architecture Summary
The implemented CPU consists of the following major components:
- Program Counter (PC)  
- Register File  
- Arithmetic Logic Unit (ALU)  
- Instruction Memory  
- Data Memory  
- Control Unit  
- Multiplexers and control signals  
- Clocked datapath  

The CPU supports RISC-style instructions, including arithmetic, logical, memory access, and branching operations. Waveforms and lab results can be found in the **Lab 6 Report**.
