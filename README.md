# `TapeoutSzn`
The road to tapeout is real. Welcome to my assignment hub!

This repository contains a list of exercises incorporated into various lab activities spanning a time period of 4 months leading to a potential tapeout! 

Design Automation to it's fullest!

# `Introduction to RISC-V ISA and GNU Compiler Toolchain`

`RISC-V` is an open `ISA` (Instruction Set Architecture) which gives any hardware designer the privilege to utilize an already existing framework to run his/her own applications while having the flexibility to tailor his piece of hardware accordingly.

---

 >An `Instruction Set Architecture` establishes a handshake between hardware and software, multiple times this bridge has often been hard to cross due to licensing difficulties surrounding giant companies like `Intel` and `ARM` owning popular ISAs like the `x86-64`, but not anymore, thanks to `RISC-V` 

---
###### An application designed through a high level language (HLL) is brought down to assembly level via a compiler. Most of the time these compilers are provided by `GCC` (GNU's Compiler Collection) and they are tailored to a specific ISA.

---
##### The assembly counterpart of an application is fed to an assembler which procures binaries (the only set of primitives that a machine can truly understand).

>Assembly language consists of a list of instructions specific to a piece of architecture. These instructions are mapped to binaries via a layer of `RTL` coding (HDL Haven) and this translates to the physical layout in a very formative flow referred to as the RTL to GDS flow.

---
The base extension to the `RISC-V ISA` consists of 47 instructions ranging from data transfer instructions to integer arithmetic instructions also involving control flow instructions in the middle.

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

The `RISC-V ISA` consists of 32 registers to maintain simplicity in the architectural setup.  
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

>Where the register pseudo names are referred to as the `ABI` (Application Binary Interface).

---
### `Lab work for RVDAY1_MYTH covers` :  
1) Sum from 1 to N compute : compiling via gcc and disassembling through `riscv64-unknown-elf-objdump` -d <object_file> with -O1 and -Ofast optimizations and proceeding to `simulate` via a `InstructionAccurate` Spike Simulator.


 
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

# `Spike Simulation and Debug`

>*What is Spike?*
>Spike is an instruction accurate RISC-V processor that can be invigorated to 32 or 64 bit utilization preferably used when modelling the execution correctness of an application.

***`Spike` allows a series of compiler flags to tag a `proxykernal` that runs `baremetal` programs.***
Spike allows the flexibility to access and view the contents of **each** register after the completion of a program.

>Instruction Accurate Simulator is a software tool used in computer architecture research and development to model the behavior of a computer's hardware at a very detailed level. This type of simulator is designed to accurately replicate the execution of individual machine instructions on a specific processor's microarchitecture.

---

# `Integer Number Representation`

This subset of this day throws light on the different `Number Systems` that are prevalent and the importance between utilizing these different data types in performing operations. 

>- Unsigned numbers, also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.
>- Range: 0 to 2^(N) - 1.


>- Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.
>- Range : -(2^(N-1)) to 2^(N-1) - 1.

---
### `Unsigned Numbers with Spike`
##### 1) `unsignedint.c`
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
---
### `Signed Numbers With Spike`
##### 2) `signedint.c`
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
# `RVDAY2_MYTH` :

---
# `Application Binary Interface`
---
## `Introduction to ABI`

An Application Binary Interface (ABI) is a set of conventions or rules that govern how functions, data structures, and system calls should be organized and accessed in a binary program or library. It defines the low-level interface between different parts of a program or between a program and the operating system. Here are the key points about an ABI:

1. **Binary Compatibility**: ABIs ensure that binary code produced by one compiler or platform can work seamlessly with code produced by another, as long as they adhere to the same ABI.
    
2. **Function Calling Convention**: ABIs specify how functions are called, including the order and location of arguments and return values, as well as how the call stack is managed during function calls.
    
3. **Register Usage**: ABIs define which registers are reserved for certain purposes (e.g., argument passing, return values, temporary storage) and how they should be managed during function calls.
    
4. **Data Layout**: ABIs specify how data structures like structs and arrays are laid out in memory, including rules for alignment and padding.
    
5. **Exception Handling**: They define how exceptions (such as hardware or software interrupts) are handled, including how control is transferred between user code and exception handlers.
    
6. **System Calls**: ABIs detail how programs interact with the operating system through system calls, including how arguments are passed and results are retrieved.
    
7. **Platform Independence**: ABIs help maintain compatibility across different platforms (e.g., different CPU architectures or operating systems) by providing a standardized interface.
    
8. **Dynamic Linking**: They cover aspects of dynamic linking, such as how shared libraries (DLLs on Windows or shared objects on Unix-based systems) are loaded and linked at runtime.
    
9. **Versioning**: Some ABIs include mechanisms for versioning so that future changes can be made without breaking compatibility with existing code.
    
10. **Documentation**: ABIs are typically documented and published, allowing developers to write code that conforms to the ABI's specifications.
    
11. **Toolchain Support**: Compilers and assemblers are designed to generate code that follows the ABI, ensuring that code produced by different tools can interoperate.
    
12. **Cross-Platform Development**: ABIs are especially important for cross-platform development, where code needs to run on multiple platforms with potentially different hardware architectures and operating systems.
    
13. **Security**: ABIs may include security-related aspects, such as buffer overflow protection mechanisms and stack canaries.
# `Memory Allocation for Double Words`
---
64-bit number (or any multi-byte value) can be loaded into memory in little-endian or big-endian. It involves understanding the byte order and arranging the bytes accordingly

1. **Little-Endian:** In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.
2. **Big-Endian:** In big-endian representation, you store the most significant byte (MSB) at the lowest memory address and the least significant byte (LSB) at the highest memory address.
# `Load, Add and Store Instructions`
---
Load, Add, and Store instructions are fundamental operations in computer architecture and assembly programming. They are often used to manipulate data within a computer's memory and registers.
Example -1  `ld x8, 16(x23)`

In this Example

- `ld` is the load double-word instruction.
- `x8` is the destination register.
- `16(x23)` is the memory address pointed to by register `x5` (base address + offset).

Example -2  `add x8, x24, x8`

In this Example

- `add` is the add instruction.
- `x8` is the destination register.
- `x24` and `x8` are the source registers.
# `Application Binary Interface LabWork!`
#### abiwork.c `c-program`


```c
#include<stdio.h>

extern int load(int x, int y);

int main()
{
  int result = 0;
  int count = 9;
  result = load(0x0, count+1);
  printf("Sum of numbers from 1 to 9 is %d\n", result);
}

```
#### assembly.c `assembly program`
```c
.section .text
.global load
.type load, @function
load:
add a4, a0, zero
add a2, a0, a1
add a3, a0, zero
loop:
add a4, a3, a4
addi a3, a3, 1
blt a3, a2, loop
add a0, a4, zero
ret
```
