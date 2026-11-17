# 32-bit RISC CPU in VHDL

A multi-cycle 32-bit CPU designed from the gate level up in VHDL, with a custom 26-instruction ISA. It has its own datapath, ALU, register set, FSM control unit and memory, and was verified in simulation and run on an Altera Cyclone IV FPGA.

Final project for **COE 608 (Computer Organization and Architecture)** at Toronto Metropolitan University. Built up across six incremental labs, from adders and registers to the full processor.

## Features

- 32-bit datapath with two general-purpose registers (A, B), carry (C) and zero (Z) flags
- 32-bit instruction register and program counter
- Three-state fetch / decode / execute control FSM
- ALU built from a hierarchy of ripple-carry adders (full adder → 4 → 16 → 32 bit) with AND, OR, add, subtract and 1-bit shift operations
- Upper/lower zero-extension units for immediates (`LUI`, `ANDI`, `ORI`)
- Separate instruction memory and data memory
- Simulation wrapper (`cpu_test_sim.vhd`) that exposes registers, flags, PC, IR and FSM state for waveform debugging

## Instruction set

| Group | Instructions |
|---|---|
| Load / store | `LDA`, `LDB`, `LDAI`, `LDBI`, `STA`, `STB`, `LUI` |
| Arithmetic | `ADD`, `ADDI`, `SUB`, `INCA`, `DECA` |
| Logic and shift | `AND`, `ANDI`, `ORI`, `ROL`, `ROR` (1-bit shifts) |
| Register and flag | `CLRA`, `CLRB`, `CLRC`, `CLRZ`, `TSTC`, `TSTZ` |
| Control flow | `JUMP`, `BEQ`, `BNE` |

The top 4 bits of each instruction select memory and branch operations. ALU operations share the `0111` prefix and use the next 4 bits to choose the operation.

## Architecture

| File | What it does |
|---|---|
| `cpu1.vhd` | Top level: connects the control unit and datapath |
| `control.vhd` | FSM control unit: decodes the instruction and drives every load, clear, mux-select and ALU-op signal |
| `data_path.vhd` | Registers, ALU, multiplexers, PC and memory interface |
| `alu.vhd` | 32-bit ALU |
| `fulladd.vhd`, `adder4.vhd`, `adder16.vhd`, `adder32.vhd`, `add.vhd` | Adder hierarchy |
| `register32.vhd`, `pc.vhd` | 32-bit register and program counter |
| `mux2to1.vhd`, `mux4to1.vhd` | Datapath multiplexers |
| `LZE.vhd`, `UZE.vhd`, `RED.vhd` | Lower/upper zero extension and address reduction |
| `data_mem.vhd`, `system_memory.vhd` | Data memory and instruction memory |
| `reset_circuit.vhd` | Reset sequencer that clears the PC and holds the datapath for a few clocks after reset |
| `cpu_test_sim.vhd` | Simulation top level with debug outputs |

## Tools

VHDL · Intel Quartus Prime · ModelSim · Altera Cyclone IV FPGA

## Results

Waveforms for each instruction and the full test program are in the [Lab 6 report](<lab 6 Report.pdf>).

## What I learned

- Splitting a processor into datapath and control, and deriving control signals per instruction per state
- Building a multi-cycle fetch/decode/execute sequence
- Verifying a CPU instruction by instruction with waveforms before moving to hardware
