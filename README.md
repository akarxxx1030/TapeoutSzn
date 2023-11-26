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

![sum1ton](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/3c0936b6-adab-41ed-b8f9-2ec3c1cc3a50)


![objdumpsum1ton](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/9bd8b9a6-8dc6-40b8-932a-e5ce40b67a39)


![sum1tonassembly](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/770a3084-0aaf-4045-a002-4a16fb80c956)

![spikedebug](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/12f6c0fa-f0ad-43b6-bf00-144bbce17712)


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
![unsignedoutput](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/a21ecf38-9a2e-44ff-8456-d6190ef8b58f)

![unsignedassembly](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/bf085c9c-2834-4add-8198-a48400148d0f)



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
![signedoutput](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/ece92f36-4749-4e30-b745-b8bb7eb7eb6f)

![signedunsignedspike](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/e6f86af0-38f9-4612-92b2-d2a64e0f589e)

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
![abispike](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/8754ede7-9ae6-4f21-bcb3-d5c0f869bbd0)


## DAY 3: Combinational and sequential optimizations

Inorder to optimise a verilog files that has submodules, We have to first flatten it, then optimize ```opt_clean -purge``` and complete the synthesis process

Here we can observe that instead of using ```and``` gate and ```or``` gates, its using ```AOI```
The synthesis sctipts can be found in the verilog folder, the same steps as above can be followed to visualize the sythesised verilog using yosys.

> Find all the verilog used in the verilog directory

### opt_check1.v
![Alt text](<Screenshot from 2023-10-28 17-28-57.png>)

### opt_check2.v
![image](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/2cee5cbe-0652-4a71-a666-0434876fde64)

### opt_check3.v

![image-1](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/7f9f45be-b4a2-4d50-bb5f-cf0d169a4430)

### opt_check4.v

![image-2](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/742453bc-8f90-4485-bedf-47bccc09c490)
### multipe_modules_opt.v
![image-3](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/94309177-11e0-4eca-b83c-1b4b66623ad8)

Inorder to optimise a verilog files that has submodules, We have to first flatten it, then optimize opt_clean -purge and complete the synthesis process

Here we can observe that instead of using 'and' gate and 'or' gates, its using 'AOI'

> The waveforms can be vizualized using gtk wave using vcd 

###  dff_const1 dff_const1_tb.v
![image-5](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/d9e7dfbe-d560-480c-9827-b34b2255872c)
![image-4](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/898cff11-5617-49d9-83ab-5310f5c192e6)

###  dff_const2 dff_const2_tb.v
![image-8](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/b9e47249-79a7-4ebc-8e1d-8e7265567b9f)
![image-7](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/83aa260c-684f-415d-bd68-6e4446cf8a79)

### dff_cosnt3 dff_const3_tb.v
![image-9](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/af28f599-079b-469b-8180-04bb0c606c2a)

![image-10](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/2d20842b-3877-45c4-9dcd-e7faf286c7b2)

### dff_const4 dff_const4_tb.v
![image-11](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/55b79b42-eb33-45a4-a65b-f99520ca736b)

![image-12](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/31b8fc91-7694-42cc-8207-e08e800169ea)

### dff_const5 dff_const5_tb.v

![image-13](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/ca6935a0-088d-46dc-b8a1-f16b2fc76f28)
![image-14](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/5c9957bb-4026-43d8-b83c-dc9fcfb7657e)

### counter_opt1.v
![image-15](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/0069ab97-65ce-4989-945e-e2fcc2788a00)

### counter_opt2.v

![image-16](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/5c6c3b9d-89e3-4758-a5a5-e3a6c1a4c44c)

>Usually a 3 bit counter requires 3 flops but since the output here is dependent on only the LSB and other 2 bits are unused. Therefore only one flop is being down and as we know that LSB toggles every clock cylce,its just using an inverter to invert the output at every clock cycle. - counter1.v dot diag shows us this

in the second one counter2 the logic is changed such a way that the output is dependent on all 3bits, it has inferred 3 ffs.

---

## DAY 4:GLS, SYnthesis solution mismatch

## Gate Level Simulation(GLS)

- used for post-synthesis verification to ensure functionality and timing requirements
- input : testbench ,synthesized netlist of a deisgn, gate level verilog models (since design now is synthesised one , it has library gate definitions in it.so we have to pass those verilog models too)
- sometimes there is a mismatch in simulation results for post-synthesis netlist that's called synthesis simulation mismatch

### Synthesis Simulation Mismatch

Reasons : 
- **Missing Sensitivity list**
- **Blocking(sequential execution) vs Non Blocking assignments(parallel Execution)**
- **Non standard verilog codeing**

### GLS Lab

```
synthesize conditional_mux and write its netlist
iverilog <Path_to_primitives.v>/primitives.v <path_to_sky130_fd_sc_hd.v>/sky130_fd_sc_hd.v <path_to_synthesized_netlist>/conditional_mux_mapped.v <path_to_original_file>/conditional_mux_tb.v -o conditional_mux_gls.out
./conditional_mux_gls.out
gtkwave conditional_mux_tb.vcd
```
On running the above command we can get the waveforms using gtk wave.

## presynthesis(above) and post-synthesis simulation(below) conditional_mux.v conditional_mux_tb.v


![image-33](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/a2d2a52b-262f-473c-920e-7f9f6bf1ab08)
![image-34](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/4f4be162-ca2b-4efa-a925-afa1e83d9a68)

> The above shows presynthesis and post-synthesis waveforms, as we can see both are so same hece we can confirms that the synthesized netlist is functionally correct

## presynthesis(above) and post-synthesis(below) bad_mux.v bad_mux_tb.v

> Checking functionality with waveforms
![image-35](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/77d1c816-fdfe-4b05-935f-c3e1de2ac8d0)

![image-37](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/68ca5cb2-110a-4e32-b45a-faa5bffbaa3f)
![image-36](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/c81dc57c-1d80-42cf-8258-5bb2f0d83dce)

## presynthesis(above) and post-synthesis(below) Blocking_error.v Blocking_error_tb.v
![image-23](https://github.com/akarxxx1030/TapeoutSzn/assets/102870828/116422d7-e3e9-4101-9440-976c5f84d431)


> find all the TB, Waveforms(vwf files) and verilog files in the verilog directory.
