# RISC-V CPU Core  

This repository contains my implementation of a **32-bit Single-Cycle RISC-V (RV32I) CPU Core** designed in **TL-Verilog** and simulated on the **Makerchip IDE**.  

The project demonstrates how the fundamental components of a processor work together to execute instructions, following the RISC-V ISA specification.  

---

## Table of Contents  
- [Overview](#overview)  
- [Implementation Plan](#implementation-plan)  
- [CPU Datapath](#cpu-datapath)  
- [Modules](#modules)  
  - [Program Counter (PC) Logic](#program-counter-pc-logic)  
  - [Instruction Memory](#instruction-memory)  
  - [Decode Logic](#decode-logic)  
  - [Register File (Read & Write)](#register-file-read--write)  
  - [Arithmetic Logic Unit (ALU)](#arithmetic-logic-unit-alu)  
  - [Data Memory (DMem)](#data-memory-dmem)  
- [Waveforms](#waveforms)  
- [Complete Code](#complete-code)  
- [Simulation](#simulation)  
- [References](#references)  

---

## Overview  
- **ISA**: RISC-V RV32I (Integer Base Instructions)  
- **Design Style**: Single-Cycle CPU  
- **HDL**: TL-Verilog  
- **Simulation Platform**: Makerchip IDE
- **FPGA Synthesis:** Xilinx Vivado (for hardware deployment)
- **Target Hardware:** Nexys A7 FPGA Board

This CPU implements the full RV32I instruction set, with working fetch, decode, execute, and writeback stages. 

Link for the Makerchip IDE Simulation of the processor core: [Makerchip IDE](https://makerchip.com/sandbox/0QWf6hoP/0P1h04V#).  

---

## CPU Datapath  
![RISC-V Datapath](Images/CPU_Diagram.png)  

---
## Implementation Plan  
1. Build **Program Counter (PC)** logic.  
2. Add **Instruction Fetch** unit.  
3. Implement **Instruction Decode** logic.  
4. Integrate **Register File** (read & write).  
5. Design **Arithmetic Logic Unit (ALU)**.  
6. Add **Data Memory (DMem)** for load/store instructions.  
7. Verify design with **test programs** and **waveform analysis**.

![RISC-V Processor Diagram](Images/RISC-V_CPU_Block_Diagram.png)  


---
## Modules  

### Program Counter (PC) Logic  
- Responsible for selecting the next instruction.  
- Supports **sequential execution**, **branches**, and **jumps**.  

![PC Logic](Images/Initial_PC_logic.png)  


### Instruction Memory  
- Stores the program instructions.  
- Fetches instructions based on PC value.  

![Instruction Memory](Images/Instruction_memory_hookup.png)  


### Decode Logic  
- Decodes the fetched instruction into its fields.  
- Identifies source registers, destination register, immediate values, and opcode.  

![Instruction Types](Images/RISC-V_Base_Instructions.png)  
![Instruction Types](Images/Instruction_types_from_opcode_6-2___instr_6-2__.png)



### Register File (Read & Write)  
- Provides fast access to operands.  
- Writes back results from ALU or memory.  

![Register File](Images/The_provided_register_file_instantiation__before_you_modify_it_.png)  


### Arithmetic Logic Unit (ALU)  
- Performs arithmetic and logical operations (add, sub, and, or, shift, etc.).  

![ALU Operations](Images/RV32I_Base_Integer_Instructions.png)  


### Data Memory (DMem)  
- Supports **load** and **store** instructions.  
- Simplified single-cycle implementation.  

![Data Memory](images/dmem.png)  

---

## Waveforms  
Waveforms showing execution of sample programs:  

![Waveform Example](Images/Waveforms.png)  

---

## Complete Code  
The **full implementation** of the single-cycle RISC-V CPU can be found in:  [`RISC-V CPU Core`](risc-v_core.tlv)  

---

## Simulation  
- The CPU is designed and simulated on the [Makerchip IDE](https://makerchip.com/sandbox/0QWf6hoP/0P1h04V#).  
- Makerchip provides both **visual datapath** diagrams and **waveform outputs**.  
![Visualisation of CPU Core](Images/Visual_CPU_Program.png)
---

## References  
- [RISC-V ISA Specification](https://riscv.org/technical/specifications/)
- [RISC-V RV32I Base Integer Instructions](https://www.cs.sfu.ca/~ashriram/Courses/CS295/assets/notebooks/RISCV/RISCV_CARD.pdf)
- *Digital Design and Computer Architecture, RISC-V Edition* – David Harris & Sarah Harris  

---

## Features Implemented

-   **Full RV32I ISA:** Supports all base integer instructions, including:
    -   Arithmetic (`ADD`, `ADDI`, `SUB`)
    -   Logical (`AND`, `OR`, `XOR`, `ANDI`, `ORI`, `XORI`)
    -   Shifts (`SLL`, `SRL`, `SRA`, `SLLI`, `SRLI`, `SRAI`)
    -   Comparisons (`SLT`, `SLTU`, `SLTI`, `SLTIU`)
    -   Loads and Stores (`LW`, `LH`, `LB`, `LBU`, `LHU`, `SW`, `SH`, `SB`)
    -   Conditional Branches (`BEQ`, `BNE`, `BLT`, `BGE`, `BLTU`, `BGEU`)
    -   Unconditional Jumps (`JAL`, `JALR`)
    -   Upper Immediate (`LUI`, `AUIPC`)
-   **Single-Cycle Design:** Each instruction is fully executed in one clock cycle.
-   **Harvard Architecture:** Uses separate memories for instructions (IMem) and data (DMem).

## Tools and Technologies

-   **HDL:** TL-Verilog
-   **Simulation:** Makerchip IDE
-   **FPGA Synthesis:** Xilinx Vivado (for hardware deployment)
-   **Target Hardware:** Nexys A7 FPGA Board


## FPGA Implementation Results

The CPU was successfully synthesized and deployed to a Xilinx Nexys A7 FPGA. The post-synthesis performance and resource utilization are as follows:

-   **Maximum Clock Frequency:** 50 MHz *(Replace with your actual result)*
-   **Slice LUTs:** 1,234 *(Replace with your actual result)*
-   **Flip-Flops:** 567 *(Replace with your actual result)*


## Acknowledgements

This project was developed based on the curriculum and labs from the "Building a RISC-V CPU Core (LFD111x)" course provided by The Linux Foundation and edX.
