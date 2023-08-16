# TapeoutSzn
The road to tapeout is real. Welcome to my assignment hub!

This repository contains a list of exercises incorporated into various lab activities spanning a time period of 4 months leading to a potential tapeout! 

Design Automation to it's fullest!

## RVDay1_MYTH_Notes

RISC-V is an open #ISA (Instruction Set Architecture) which gives any hardware designer the privilege to utilize an already existing framework to run his/her own applications while having the flexibility to tailor his piece of hardware accordingly.

---

>An "Instruction Set Architecture" establishes a handshake between hardware and software, multiple times this bridge has often been hard to cross due to licensing difficulties surrounding giant companies like #Intel and #ARM owning popular ISAs like the #x86-64, but not anymore, thanks to #RISC-V 

---
###### An application designed through a high level language (HLL) is brought down to assembly level via a compiler. Most of the time these compilers are provided by #GCC (GNU's Compiler Collection) and they are tailored to a specific ISA.
---
##### The assembly counterpart of an application is fed to an assembler which procures binaries (the only set of primitives that a machine can truly understand).

>Assembly language consists of a list of instructions specific to a piece of architecture. These instructions are mapped to binaries via a layer of #RTL coding (HDL Haven) and this translates to the physical layout in a very formative flow referred to as the RTL to GDS flow.

---
The base extension to the RISC-V ISA consists of 47 instructions ranging from data transfer instructions to integer arithmetic instructions also involving control flow instructions in the middle.

Similarly, other extensions that exist for various functionalities are :  
#### M - Multiplication
#### A - Atomics
#### F - Floating Points
#### D - Double Precision
#### C - Compressed Alternative

---

>RV32 refers to 32 bit instruction decoding while the RV64 refers to the 64 bit instruction encoding. The RV64IMAFDC translates to RV64GC where G stands for the General ISA Specs.

The RISC-V ISA consists of 32 registers to maintain simplicity in the architectural setup.  

x0-x31 : Mapping Terminology  
x0 : Zero Register
x1 : Return Address Register
x2 : Stack Pointer
x3 : Global Pointer
x4 : Thread Pointer
x5-x7 : Temporary Registers
x8,x9 : Saved Registers  
x10-x17 : Argument Registers
x18-x27 : Saved Registers
x28-x31 : Temporary Registers

>Where the register pseudo names are referred to as the #ABI (Application Binary Interface).

---
### Lab work for RVDAY1_MYTH covers :  
1) Sum from 1 to N compute : compiling via gcc and disassembling through #riscv64-unknown-elf-objdump -d <object_file> with -O1 and -Ofast optimizations and proceeding to #simulate via a #InstructionAccurate Spike Simulator.
---

