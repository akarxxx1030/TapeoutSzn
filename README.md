# TapeoutSzn
The road to tapeout is real. Welcome to my assignment hub!

This repository contains a list of exercises incorporated into various lab activities spanning a time period of 4 months leading to a potential tapeout! 

Design Automation to it's fullest!

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
``` 
M - Multiplication
A - Atomics
F - Floating Points
D - Double Precision
C - Compressed Alternative
```

---

>RV32 refers to 32 bit instruction decoding while the RV64 refers to the 64 bit instruction encoding. The RV64IMAFDC translates to RV64GC where G stands for the General ISA Specs.

The RISC-V ISA consists of 32 registers to maintain simplicity in the architectural setup.  
```
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
```

>Where the register pseudo names are referred to as the #ABI (Application Binary Interface).

---
### Lab work for RVDAY1_MYTH covers :  
1) Sum from 1 to N compute : compiling via gcc and disassembling through #riscv64-unknown-elf-objdump -d <object_file> with -O1 and -Ofast optimizations and proceeding to #simulate via a #InstructionAccurate Spike Simulator.


 
	 The simulation optimization level is varied by switching between -O1,-O2, -O3 and -OFast utilising the riscv64-unknown-elf-objdump executable. The executable helps in disassembling the application with the -d flThe C code followed for the implementation is given below :
```c
#include<stdio.h>
int main()
{
int num,temp;
printf("Enter a number\n");
scanf("%d",&num);
for(int i=0;i<num;i++)
temp+=1;
printf("%d\n",temp);
}
```
---

# Spike Simulation and Debug

>What is Spike?
>Spike is an instruction accurate RISC-V processor that can be invigorated to 32 or 64 bit utilization preferably used when modelling the execution correctness of an application.

***Spike allows a series of compiler flags to tag a #proxykernal that runs #baremetal programs.***
Spike allows the flexibility to access and view the contents of **each** register after the completion of a program.

>Instruction Accurate Simulator is a software tool used in computer architecture research and development to model the behavior of a computer's hardware at a very detailed level. This type of simulator is designed to accurately replicate the execution of individual machine instructions on a specific processor's microarchitecture.

---

# Integer Number Representation

This subset of this day throws light on the different #NumberSystems that are prevalent and the importance between utilizing these different data types in performing operations. 

>- Unsigned numbers, also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.
>- Range: 0 to 2^(N) - 1.


>- Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.
>- Range : -(2^(N-1)) to 2^(N-1) - 1.

---
### Unsigned Numbers with Spike
##### 1) unsignedint.c
```c
#include <stdio.h>
#include <math.h>

int main(){
	unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
	unsigned long long int min = (unsigned long long int) (pow(2,64) *(-1));
	printf("lowest number represented by unsigned 64-bit integer is %llu\n",min);
	printf("highest number represented by unsigned 64-bit integer is %llu\n",max);
	return 0;
}
```
##### 2) signedint.c
```c
#include <stdio.h>
#include <math.h>

int main(){
	long long int max = (long long int) (pow(2,63) -1);
	long long int min = (long long int) (pow(2,63) *(-1));
	printf("lowest number represented by signed 64-bit integer is %lld\n",min);
	printf("highest number represented by signed 64-bit integer is %lld\n",max);
	return 0;
}
```
---
