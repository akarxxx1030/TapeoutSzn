# `TapeoutSzn`👏
The road to tapeout is real. Welcome to my assignment hub!

This repository contains a list of exercises incorporated into various lab activities spanning a time period of 4 months leading to a potential tapeout! 

Design Automation to it's fullest!

![Automation!](https://1401700980.rsc.cdn77.org/data/images/full/12204/silicon-wafer.jpg)


# `Introduction to RISC-V ISA and GNU Compiler Toolchain` 🤖

`RISC-V` is an open `ISA` (Instruction Set Architecture) which gives any hardware designer the privilege to utilize an already existing framework to run his/her own applications while having the flexibility to tailor his piece of hardware accordingly.

![RISC-V!](http://blog.trinamic.com/wp-content/uploads/2017/11/20151229-riscv.jpg)

---

 >An `Instruction Set Architecture` establishes a handshake between hardware and software, multiple times this bridge has often been hard to cross due to licensing difficulties surrounding giant companies like `Intel` and `ARM` owning popular ISAs like the `x86-64`, but not anymore, thanks to `RISC-V` 

![The RISC-V Flow!](https://user-images.githubusercontent.com/142098395/261306361-4eabe0b7-4581-419b-88e7-84c7ac1dac8e.png)

---
###### An application designed through a high level language (HLL) is brought down to assembly level via a compiler. Most of the time these compilers are provided by `GCC` (GNU's Compiler Collection) and they are tailored to a specific ISA.
![Compilation to Baremetal!](https://user-images.githubusercontent.com/103078929/261504893-1d76b7ef-cac9-4331-9190-31af36525e0c.png)

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

![RISC-V's ABI Interface, simplistic!](https://camo.githubusercontent.com/c04ed42276c00a928a47b5a8220df02f1fb4a123453509f9484cd5940fb25299/68747470733a2f2f7765622e656563732e75746b2e6564752f7e736d61727a312f636f75727365732f6563653335362f6e6f7465732f726973632f696d67732f72656766696c652e706e67)

---

### Lab work for RVDAY1_MYTH📚
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

![sum1ton.c on Spike!](file:///home/aakarsh/Pictures/Screenshots/sum1ton.png)

![objdump sum1ton.c](file:///home/aakarsh/Pictures/Screenshots/objdumpsum1ton.png)

![Assembly Breakdown of sum1ton.c](file:///home/aakarsh/Pictures/Screenshots/sum1tonassembly.png)

![Debug With Spike - A Glimpse!](file:///home/aakarsh/Pictures/Screenshots/spikedebug.png)

# Spike Simulation and Debug 🐛

>*What is Spike?*
>Spike is an instruction accurate RISC-V processor that can be invigorated to 32 or 64 bit utilization preferably used when modelling the execution correctness of an application.

***`Spike` allows a series of compiler flags to tag a `proxykernal` that runs `baremetal` programs.***
Spike allows the flexibility to access and view the contents of **each** register after the completion of a program.

![Spike's Environment](https://cdn-ak.f.st-hatena.com/images/fotolife/m/msyksphinz/20180611/20180611010051.png)

>Instruction Accurate Simulator is a software tool used in computer architecture research and development to model the behavior of a computer's hardware at a very detailed level. This type of simulator is designed to accurately replicate the execution of individual machine instructions on a specific processor's microarchitecture.

---

# `Integer Number Representation`🕐

This subset of this day throws light on the different `Number Systems` that are prevalent and the importance between utilizing these different data types in performing operations. 

>- Unsigned numbers, also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.
>- Range: 0 to 2^(N) - 1.


>- Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.
>- Range : -(2^(N-1)) to 2^(N-1) - 1.

---
### Unsigned Numbers with Spike
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
![Unsigned Output!](file:///home/aakarsh/Pictures/Screenshots/unsignedoutput.png)
![Unsigned Assembly Breakdown!](file:///home/aakarsh/Pictures/Screenshots/unsignedassembly.png)


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
 ![Signed Output!](file:///home/aakarsh/Pictures/Screenshots/signedoutput.png)
 ![Signed-Unsigned On Spike!](file:///home/aakarsh/Pictures/Screenshots/signedunsignedspike.png)
---
# RVDAY2_MYTH🥳

---
# Application Binary Interface 🖥️
---
## Introduction to ABI 

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
# Memory Allocation for Double Words🤔
---
->64-bit number (or any multi-byte value) can be loaded into memory in little-endian or big-endian. It involves understanding the byte order and arranging the bytes accordingly

1. **Little-Endian:** In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.

![Little Endian](https://user-images.githubusercontent.com/103078929/261368957-307fabf6-7f58-4337-8171-6d62d99a4386.png)

2. **Big-Endian:** In big-endian representation, you store the most significant byte (MSB) at the lowest memory address and the least significant byte (LSB) at the highest memory address.

![Big Endian!](https://user-images.githubusercontent.com/103078929/261369046-aa53e082-5878-4e3f-948a-f6f080ed0ed2.png)

---
### RISC-V Instructions🥇

RISC-V instructions can be categorized into different categories based on their functionality. Here are some common types of RISC-V instructions:

- **R-Type Instructions:** These are used for arithmetic and logic operations between two source registers, storing the result in a destination register. Common R-type instructions include:
    
    - `add`: Addition
    - `sub`: Subtraction
    - `and`: Bitwise AND
    - `or`: Bitwise OR
    - `xor`: Bitwise XOR
    - `slt`: Set Less Than (signed)
    - `sltu`: Set Less Than (unsigned)
- **I-Type Instructions:** These are used for arithmetic and logic operations that involve an immediate value (constant) and a source register. Common I-type instructions include:
    
    - `addi`: Add Immediate
    - `andi`: Bitwise AND with Immediate
    - `ori`: Bitwise OR with Immediate
    - `xori`: Bitwise XOR with Immediate
    - `lw`: Load Word (load data from memory)
    - `sw`: Store Word (store data to memory)
    - `beq`: Branch if Equal
    - `bne`: Branch if Not Equal
- **S-Type Instructions:** These are similar to I-type instructions but are used for storing values from a source register into memory. Common S-type instructions include:
    
    - `sb`: Store Byte
    - `sh`: Store Halfword
    - `sw`: Store Word
- **U-Type Instructions:** These are used for setting large immediate values into registers or for jumping to an absolute address. Common U-type instructions include:
    
    - `lui`: Load Upper Immediate (set the upper bits of a register)
    - `auipc`: Add Upper Immediate to PC (used for address calculations)
- J-Type Instructions: These are used for jumping or branching to different program locations. Common J-type instructions include:
    
    - `jal`: Jump and Link (used for function calls)
    - `jalr`: Jump and Link Register (used for function calls)
- **F-Type and D-Type Instructions (Floating-Point):** These instructions are used for floating-point arithmetic and include various operations like addition, multiplication, and comparison. These instructions typically have an 'F' or 'D' prefix to indicate single-precision or double-precision floating-point operations.
    
    - `fadd.s`: Single-precision floating-point addition
    - `fmul.d`: Double-precision floating-point multiplication
    - `fcmp.s`: Single-precision floating-point comparison
- **RV64 and RV32 Variants:** RISC-V can be configured in different bit-widths, with RV64 being a 64-bit architecture and RV32 being a 32-bit architecture. Instructions for these variants have slightly different encoding to accommodate the different data widths.
![Various Instruction Formats within the RISC-V Spectrum](https://camo.githubusercontent.com/21a8aa2033a3a0233295924dbb9548c06a86ad71665fc9805e56528e95ecf7db/68747470733a2f2f6465766f70656469612e6f72672f696d616765732f61727469636c652f3131302f333830382e313533353330313633362e706e67)

# Load, Add and Store Instructions🌴
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
# Application Binary Interface LabWork!
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
#### assembly.s `assembly program`
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
![ABI with Spike!](file:///home/aakarsh/Pictures/Screenshots/abispike.png)

