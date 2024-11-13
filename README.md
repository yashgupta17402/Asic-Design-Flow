
## Table of Contents
- [Assignment 1](#assignment-1)
- [Assignment 2](#assignment-2)
- [Assignment 3](#assignment-3)
- [Assignment 4](#assignment-4)
- [Assignment 5](#assignment-5)
- [Assignment 6](#assignment-6)
- [Assignment 7](#assignment-7)
- [Assignment 8](#assignment-8)
- [Assignment 9](#assignment-9)
- [Assignment 10](#assignment-10)
  - [Day_1](#Day-1)
  - [Day 2](#Day-2)
  - [Day 3](#Day-3)
  - [Day 4](#Day-4)
- [Assignment 11](#assignment-11)
- [Assignment 12](#assignment-12)
- [Assignment 13](#assignment-13)
- [Assignment 14](#assignment-14)
## Assignment 1

## GCC Compilation: C Program
### Step 1
* In the Linux Environment, create a new C Program file using any editor.
* Command used to create C program: gedit filename.c 
  1. **Code :**
    ```c
    #include <stdio.h>

    int main() {
        int i, n=200, sum=0;
        for(i=1; i<=n; ){
          sum = sum + i;
          i=i+1;
        }
        printf("The sum from 1 to %d is %d\n", n, sum);
        return 0;
    }
    ```
* Save the program and compile your code in the terminal window using GCC compiler.
  
  
![Screenshot from 2024-08-08 00-57-50](https://github.com/user-attachments/assets/0d5b0ae4-f21d-4d82-a1cb-e196cfcc9c6c)


### Step 2
Run the executable program and see the output in the terminal window.
### Output
The picture below represents the compiling  C code using gcc and  running  its output using a.out

![Screenshot from 2024-08-08 00-59-32](https://github.com/user-attachments/assets/08e41098-b476-4f8a-ab9b-3fc5b6038c44)




## RISC-V Compilation:C Program
### Step 1
1. **Code Snippet:**
    ```c
    #include <stdio.h>

    int main() {
        int i, n=200, sum=0;
        for(i=1; i<=n; ){
          sum = sum + i;
          i=i+1;
        }
        printf("The sum from 1 to %d is %d\n", n, sum);
        return 0;
    }
    ```
* Compile the C code on RISC-V compiler
  ![Screenshot from 2024-08-08 01-01-01](https://github.com/user-attachments/assets/fcf7aa98-0f4a-43c9-9416-c131f6cb734f)

  

* Now create the object file (.o) ,which is the output of the compiler as shown in the procedure shown below.
  
![Screenshot from 2024-08-08 01-01-25](https://github.com/user-attachments/assets/a991b66e-bcf8-4676-8127-4657a8882f16)
![Screenshot from 2024-08-08 01-01-29](https://github.com/user-attachments/assets/4aef3604-22b4-4854-83e2-08a9d06ee7a8)


### Step 2
* Run the executable program and see the output in the terminal window.
![Screenshot from 2024-08-08 01-02-03](https://github.com/user-attachments/assets/88d0d7dc-2457-4412-afc5-436743236450)

* For the "main" section, we can calculate the number of instructions  by counting each individual instruction.

* E.g.: No. of instruction in main block = 15 instructions

### Step 3
* Compile the code again with the compiler flag set as **-Ofast** and observe the generated assembly code
![Screenshot from 2024-08-08 01-02-38](https://github.com/user-attachments/assets/3cb7cc10-20e5-4848-b912-1d94889d1b2d)


* Assembly code generated with **-Ofast** compiler flag
![Screenshot from 2024-08-08 01-03-04](https://github.com/user-attachments/assets/682644af-f0db-4c8d-b393-2bc8fee9ec28)


We can see that the number of instructions has decreased from 15 to 12 compared to the previous case.
The -O1 optimization flag provides moderate code optimization, adhering closely to standards, while the -Ofast flag offers more aggressive optimization, aiming for the highest possible performance but potentially deviating from some standards to achieve better results.

  
## Assignment 2
## RISC-V COMPILER OUTPUT and DEBUGGING

Find the output of the C program on the RISC V Compiler using the Spike command and debug the code

## Check the Output and compare with previous output.
We are going to have find the result of n numbers on the RISCV compiler using the SPIKE command instead of gcc and risc-v compiler.

### Code for compiling the objdump file
```bash
spike pk 1tonsum.o
```
### The compiled code using SPIKE command along with object dump file
Similar result for GCC and RISCV compiler when run the program
![Screenshot from 2024-08-08 01-50-32](https://github.com/user-attachments/assets/54c475c9-cd8c-4e37-896f-f8e2b89fcf8c)



## Debug using SPIKE debugger

### Code for debugging the assembly code 
```bash
spike -d pk 1tonsum.o
```
We will allow the Spike debugger to run until the main function, specifically until the 100b0 instruction. After that, we will manually continue debugging and inspect the a0 register before and after the execution. We observe that the instruction lui a0, 0x21 updates the a0 register from 0x0000000000000000 to 0x000000000005000
```bash
until pc 0 100b0
```
Next, we will manually debug the next instruction i.e., addi sp, sp, -16. This instruction decrements the stack pointer (sp) by 16. Before executing this instruction, the sp register held the value 0x0000003ffffffb50, which is then updated to 0x0000003ffffffb40.
```bash
reg 0 sp
```
In the assembly code we can see that the value of the stack pointer is being reduced by 10 in hexadecimal we is equivalent to being reduced by 16 in decimal notation.
![Screenshot from 2024-08-08 02-42-11](https://github.com/user-attachments/assets/9737be79-fe40-4483-9da5-37173c90a137)

![Screenshot from 2024-08-08 02-02-21](https://github.com/user-attachments/assets/3720c1a1-8ecb-4ce7-b016-ef805c53e284)


## The same thing repeats  for -O1(as done for -Ofast earlier) 

```bash
until pc 0 10184
```
![Screenshot from 2024-08-08 02-23-26](https://github.com/user-attachments/assets/cb42587b-2894-4029-93f8-ae2ec6bdc9a6)
![Screenshot from 2024-08-08 02-23-50](https://github.com/user-attachments/assets/658dcd0f-13fd-4d2e-833d-91de4f740ab2)
![Screenshot from 2024-08-08 02-25-02](https://github.com/user-attachments/assets/76eea115-4992-41a9-8950-fe8bd80864f9)

## Assignment 3

###  Identifying Instruction Types

#### As the activity suggests, intruction types are being indentified for the instructions provided. The 32bit code is identified to do so. Each instruction type has it's own instruction format. 

Instruction formats act as a blueprint connecting the assembly language and the hardware. When the assembly language issues a command, the hardware is programmed to execute it according to a predefined format. These formats are encoded in binary sequences, which define aspects like the type of operation and the data's address. The hardware relies on these sequences to correctly perform the requested tasks.

There exists 6 types of instruction formats in RISCV.

![instruction_types_f](https://github.com/user-attachments/assets/523f7129-a80d-42c4-9c7b-6a5305139459)


### 1. R-Type (Register Type)
- **Purpose**: Used for arithmetic and logical operations between registers.
- **Fields**:
  - **Opcode**: Operation code that specifies the instruction type.
  - **Source Registers**: Two registers involved in the operation.
  - **Destination Register**: Register where the result is stored.
  - **Function Code**: Specifies the exact operation to be performed.

### 2. I-Type (Immediate Type)
- **Purpose**: Supports operations involving a constant value (immediate) and a register.
- **Fields**:
  - **Opcode**: Operation code.
  - **Source Register**: Register used in the operation.
  - **Immediate Value**: Constant value used in the operation.
  - **Destination Register**: Register where the result is stored or loaded.

### 3. S-Type (Store Type)
- **Purpose**: Used for storing data from a register into memory.
- **Fields**:
  - **Opcode**: Operation code.
  - **Source Registers**: Register containing the data to be stored.
  - **Offset (Immediate)**: Specifies the memory address offset for storing the data.

### 4. B-Type (Branch Type)
- **Purpose**: Handles conditional branching based on register comparison.
- **Fields**:
  - **Opcode**: Operation code.
  - **Source Registers**: Two registers compared to determine the branch condition.
  - **Immediate Value**: Branch target address relative to the current position.

### 5. U-Type (Upper Immediate Type)
- **Purpose**: Loads large immediate values into a register.
- **Fields**:
  - **Opcode**: Operation code.
  - **Immediate Value**: 20-bit value shifted to the upper 20 bits of the destination register.

### 6. J-Type (Jump Type)
- **Purpose**: Executes jumps to a specified address.
- **Fields**:
  - **Opcode**: Operation code.
  - **Immediate Value**: 20-bit address specifying the jump target.

Each instruction format in RISC-V is designed to streamline instruction encoding and processing, enabling efficient execution of a wide range of operations.



   
  

  ## RISC-V Instructions 

Below is a detailed representation of various RISC-V instructions, including their types, encodings, and hexadecimal values.

#### ADD `r1, r2, r3`
- **Instruction Type:** R-Type
- **Opcode:** `0110011`
- **Destination Register (rd):** `r1 (00001)`
- **Source Register 1 (rs1):** `r2 (00010)`
- **Source Register 2 (rs2):** `r3 (00110)`
- **Function Code (func3):** `000`
- **Function Code (func7):** `0000000`
- **Binary Instruction:** `0000000 00110 00010 000 00001 0110011`
- **Hexadecimal Code:** `0x006100B3

#### SUB `r3, r1, r2`
- **Instruction Type:** R-Type
- **Opcode:** `0110011`
- **Destination Register (rd):** `r3 (00110)`
- **Source Register 1 (rs1):** `r1 (00001)`
- **Source Register 2 (rs2):** `r2 (00010)`
- **Function Code (func3):** `000`
- **Function Code (func7):** `0100000`
- **Binary Instruction:** `0100000 00010 00001 000 00110 0110011`
- **Hexadecimal Code:** `0x40208333`

#### AND `r2, r1, r3`
- **Instruction Type:** R-Type
- **Opcode:** `0110011`
- **Destination Register (rd):** `r2 (00010)`
- **Source Register 1 (rs1):** `r1 (00001)`
- **Source Register 2 (rs2):** `r3 (00011)`
- **Function Code (func3):** `111`
- **Function Code (func7):** `0000000`
- **Binary Instruction:** `0000000 00011 00001 111 00010 0110011`
- **Hexadecimal Code:** `0x0030F133`

#### OR `r8, r2, r5`
- **Instruction Type:** R-Type
- **Opcode:** `0110011`
- **Destination Register (rd):** `r8 (01000)`
- **Source Register 1 (rs1):** `r2 (00010)`
- **Source Register 2 (rs2):** `r5 (00101)`
- **Function Code (func3):** `110`
- **Function Code (func7):** `0000000`
- **Binary Instruction:** `0000000 00101 00010 110 01000 0110011`
- **Hexadecimal Code:** `0x00516433

#### XOR `r8, r1, r4`
- **Instruction Type:** R-Type
- **Opcode:** `0110011`
- **Destination Register (rd):** `r8 (01000)`
- **Source Register 1 (rs1):** `r1 (00001)`
- **Source Register 2 (rs2):** `r4 (00100)`
- **Function Code (func3):** `100`
- **Function Code (func7):** `0000000`
- **Binary Instruction:** `0000000 00100 00001 100 01000 0110011`
- **Hexadecimal Code:** `0x0040C433

#### SLT `r10, r2, r4`
- **Instruction Type:** R-Type
- **Opcode:** `0110011`
- **Destination Register (rd):** `r10 (01100)`
- **Source Register 1 (rs1):** `r2 (00010)`
- **Source Register 2 (rs2):** `r4 (00100)`
- **Function Code (func3):** `010`
- **Function Code (func7):** `0000000`
- **Binary Instruction:** `0000000 00100 00010 010 01100 0110011`
- **Hexadecimal Code:** `0x00412633

#### ADDI `r12, r3, 5`
- **Instruction Type:** I-Type
- **Opcode:** `0010011`
- **Destination Register (rd):** `r12 (01100)`
- **Source Register 1 (rs1):** `r3 (00110)`
- **Immediate (imm[11:0]):** `5 (000000000101)`
- **Function Code (func3):** `000`
- **Binary Instruction:** `000000000101 00110 000 01100 0010011`
- **Hexadecimal Code:** `0x00530613

#### SW `r3, r1, 4`
- **Instruction Type:** S-Type
- **Opcode:** `0100011`
- **Source Register 2 (rs2):** `r3 (00100)`
- **Source Register 1 (rs1):** `r1 (00001)`
- **Immediate (imm[11:0]):** `4 (000000000100)`
- **Function Code (func3):** `010`
- **Binary Instruction:** `0000000 00100 00001 010 00100 0100011`
- **Hexadecimal Code:** `0x0040A223

#### SRL `r16, r11, r2`
- **Instruction Type:** R-Type
- **Opcode:** `0110011`
- **Destination Register (rd):** `r16 (10000)`
- **Source Register 1 (rs1):** `r11 (01011)`
- **Source Register 2 (rs2):** `r2 (00010)`
- **Function Code (func3):** `101`
- **Function Code (func7):** `0000000`
- **Binary Instruction:** `0000000 00010 01011 101 10000 0110011`
- **Hexadecimal Code:** `0x0025D833

#### BNE `r0, r1, 20`
- **Instruction Type:** B-Type
- **Opcode:** `1100011`
- **Source Register 1 (rs1):** `r0 (00000)`
- **Source Register 2 (rs2):** `r1 (00001)`
- **Immediate (imm[12:1]):** `20 (000000010100)`
- **Function Code (func3):** `001`
- **Binary Instruction:** `0 000001 00001 00000 001 0100 0 1100011`
- **Hexadecimal Code:** `0x02101463`

#### BEQ `r0, r0, 15`
- **Instruction Type:** B-Type
- **Opcode:** `1100011`
- **Source Register 1 (rs1):** `r0 (00000)`
- **Source Register 2 (rs2):** `r0 (00000)`
- **Immediate (imm[12:1]):** `15 (000000001111)`
- **Function Code (func3):** `000`
- **Binary Instruction:** `0 000000 00000 00000 000 1111 0 1100011`
- **Hexadecimal Code:** `0x00000F63`

#### LW `r13, r11, 2`
- **Instruction Type:** I-Type
- **Opcode:** `0000011`
- **Destination Register (rd):** `r13 (01101)`
- **Source Register 1 (rs1):** `r11 (01011)`
- **Immediate (imm[11:0]):** `2 (000000000010)`
- **Function Code (func3):** `010`
- **Binary Instruction:** `000000000010 01011 010 01101 0000011`
- **Hexadecimal Code:** `0x0025A683

#### SLL `r15, r11, r2`
- **Instruction Type:** R-Type
- **Opcode:** `0110011`
- **Destination Register (rd):** `r15 (01111)`
- **Source Register 1 (rs1):** `r11 (01011)`
- **Source Register 2 (rs2):** `r2 (00010)`
- **Function Code (func3):** `001`
- **Function Code (func7):** `0000000`
- **Binary Instruction:** `0000000 00010 01011 001 01111 0110011`
- **Hexadecimal Code:** `0x002597B3



## RISC-V Instructions Summary

This table provides details for various RISC-V instructions, including their formats and 32-bit encoding.

| **Instruction** | **Opcode** | **rd** | **rs1** | **rs2** | **func3** | **func7** | **Type** | **32-Bit Encoding** |
|-----------------|------------|--------|---------|---------|-----------|-----------|----------|---------------------|
| ADD r1, r2, r3  | 0110011    | 00001  | 00010   | 00110   | 000       | 0000000   | R        | 0000000_00110_00010_000_00001_0110011 |
| SUB r3, r1, r2  | 0110011    | 00110  | 00001   | 00010   | 000       | 0100000   | R        | 0100000_00010_00001_000_00110_0110011 |
| AND r2, r1, r3  | 0110011    | 00010  | 00001   | 00011   | 111       | 0000000   | R        | 0000000_00011_00001_111_00010_0110011 |
| OR r8, r2, r5   | 0110011    | 01000  | 00010   | 00101   | 110       | 0000000   | R        | 0000000_00101_00010_110_01000_0110011 |
| XOR r8, r1, r4  | 0110011    | 01000  | 00001   | 00100   | 100       | 0000000   | R        | 0000000_00100_00001_100_01000_0110011 |
| SLT r10, r2, r4 | 0110011    | 01100  | 00010   | 00100   | 010       | 0000000   | R        | 0000000_00100_00010_010_01100_0110011 |
| ADDI r12, r3, 5 | 0010011    | 01100  | 00110   | N/A     | 000       | N/A       | I        | 000000000101_00001_000_00110_0010011 |
| SW r3, r1, 4    | 0100011    | N/A    | 00001   | 00100   | 010       | N/A       | S        | 0000000_00100_00001_010_0001_0100011 |
| SRL r16, r11, r2| 0110011    | 10000  | 01011   | 00010   | 101       | 0000000   | R        | 0000000_00010_01011_101_10000_0110011 |
| BNE r0, r1, 20  | 1100011    | N/A    | 00000   | 00001   | 001       | N/A       | B        | 0_000001_00001_00000_001_1010_0_1100011 |
| BEQ r0, r0, 15  | 1100011    | N/A    | 00000   | 00000   | 000       | N/A       | B        | 0_000000_00000_00000_000_1111_0_1100011 |
| LW r13, r11, 2  | 0000011    | 01101  | 01011   | N/A     | 010       | N/A       | I        | 000000000010_01011_010_01101_0000011 |
| SLL r15, r11, r2| 0110011    | 01111  | 01011   | 00010   | 001       | 0000000   | R        | 0000000_00010_01011_001_01111_0110011 |

**Note**: The 32-bit encodings are represented in binary and grouped for readability.

## Assignment 4

Verilog code where instructions are defined:
![Untitled design](https://github.com/user-attachments/assets/ad0ce846-85b5-4919-8730-ff67c673294d)



Below are hardcoded ISA's and Bit Patterns of instructions in provided  verilog code.



This table maps the standard RISC-V ISA to the hardcoded ISA values used in the project, including the bit patterns.

| S. no. | Operation          | Standard RISCV ISA | Hardcoded ISA | Hardcoded Bit Pattern                             |
|--------|--------------------|---------------------|---------------|----------------------------------------------------|
| 1      | ADD R6, R2, R1     | 32'h00110333        | 32'h02208300  | 0000001 00010 00001 000 00110 0000000            |
| 2      | SUB R7, R1, R2     | 32'h402083b3        | 32'h02209380  | 0000001 00010 00001 001 00111 0000000            |
| 3      | AND R8, R1, R3     | 32'h0030f433        | 32'h0230a400  | 0000001 00011 00001 010 01000 0000000            |
| 4      | OR R9, R2, R5      | 32'h005164b3        | 32'h02513480  | 0000001 00101 00010 011 01001 0000000            |
| 5      | XOR R10, R1, R4    | 32'h0040c533        | 32'h0240c500  | 0000001 00100 00001 100 01010 0000000            |
| 6      | SLT R1, R2, R4     | 32'h0045a0b3        | 32'h02415580  | 0000001 00100 00010 101 01011 0000000            |
| 7      | ADDI R12, R4, 5    | 32'h004120b3        | 32'h00520600  | 000000000101 00100 000 01100 0000000             |
| 8      | BEQ R0, R0, 15     | 32'h00000f63        | 32'h00f00002  | 0 000000 01111 00000 000 0000 0 0000010          |
| 9      | SW R3, R1, 2       | 32'h0030a123        | 32'h00209181  | 0000000 00010 00001 001 00011 0000001            |
| 10     | LW R13, R1, 2      | 32'h0020a683        | 32'h00208681  | 000000000010 00001 000 01101 0000001             |
| 11     | SRL R16, R14, R2   | 32'h0030a123        | 32'h00271803  | 0000000 00010 01110 001 10000 0000011            |
| 12     | SLL R15, R1, R2    | 32'h002097b3        | 32'h00208783  | 0000000 00010 00001 000 01111 0000011            |


Verilog code of Testbench:
![Screenshot from 2024-08-12 15-04-03](https://github.com/user-attachments/assets/b559b677-1649-4ae2-8cb7-eae060c66beb)

Steps to run code :
<br>
Create a verilog file and testbench.Then create the dump file.Then run  GTKWave.
<br>
![Screenshot from 2024-08-12 15-05-31](https://github.com/user-attachments/assets/a87b6994-e690-4f62-aac4-c294d7fa7419)


 ```
gedit 32rv.v
gedit 32rv_test_bench.v
iverilog -o 32rv 32rv.v 32rv_test_bench.v
```
 ```
./32rv
```
 ```
gtkwave iiitb_rv32i.vcd
```
# Output of instruction in Waveform(GTKWAVE):

ADD R6, R2, R1    <br>

![Screenshot from 2024-08-12 17-47-12](https://github.com/user-attachments/assets/10d3af07-dfa7-4217-ad92-392c552e7480)

SUB R7, R1, R2     <br>

 ![Screenshot from 2024-08-12 17-47-34](https://github.com/user-attachments/assets/3018d5fa-2ee2-4eae-97bf-83f2d76b4257)

AND R8, R1, R3    <br>
 
![Screenshot from 2024-08-12 17-47-41](https://github.com/user-attachments/assets/8c67f57c-af31-45a9-887a-f56ee488f504)

OR R9, R2, R5      <br>

![Screenshot from 2024-08-12 17-47-53](https://github.com/user-attachments/assets/1ec3201c-e398-4836-b6c2-3640b4d69388)

XOR R10, R1, R4   <br>
 
 ![Screenshot from 2024-08-12 17-48-06](https://github.com/user-attachments/assets/6f7bbcf7-7bb9-4395-9559-9e3be667ad78)

SLT R1, R2, R4     <br>

 ![Screenshot from 2024-08-12 17-48-13](https://github.com/user-attachments/assets/616bce1b-d634-49b5-ab11-2601d8fa1d2b)

ADDI R12, R4, 5   <br>

![Screenshot from 2024-08-12 17-48-20](https://github.com/user-attachments/assets/83a9b641-3c95-408a-a920-05a5c67432c5)

BEQ R0, R0, 15     <br>
![Screenshot from 2024-08-12 17-49-03](https://github.com/user-attachments/assets/e1a9ee4c-7557-4755-9623-7c81f5b0d17b)


SW R3, R1, 2      <br>
![Screenshot from 2024-08-12 17-48-26](https://github.com/user-attachments/assets/3119ee7d-c025-4ed8-85c6-c10aa28455d5)


LW R13, R1, 2     <br>
![Screenshot from 2024-08-12 17-48-39](https://github.com/user-attachments/assets/5a58aa2b-dcf6-4afc-8795-091ffa507d17)

OVERALL WAVEFORM <br>


![Screenshot from 2024-08-12 17-50-54](https://github.com/user-attachments/assets/1582786d-1cac-4989-a777-d75bee547527)


  
## Assignment 5

### Step 1
* In the Linux Environment, create a new C Program file using any editor.
* Command used to create C program: gedit filename.c 
  1. **Code :**
 ```c
    #include <stdio.h>
#include <math.h>

// Function prototypes
int binaryProduct(int, int);
long binaryToDecimal(long binary);

int main()
{
    long binary1, binary2, multiply = 0;
    int digit, factor = 1;

    //printf("Enter the first binary number: ");
    //scanf("%ld", &binary1);
    binary1=11;
    binary2=10;
    //printf("Enter the second binary number: ");
    //scanf("%ld", &binary2);

    // Store the original binary numbers for later use
    long originalBinary1 = binary1;
    long originalBinary2 = binary2;

    while (binary2 != 0)
    {
        digit =  binary2 % 10;
        if (digit == 1)
        {
            binary1 = binary1 * factor;
            multiply = binaryProduct(binary1, multiply);
        }
        else
            binary1 = binary1 * factor;
        binary2 = binary2 / 10;
        factor = 10;
    }

    printf("Binary1: %ld (Decimal: %ld)\n", originalBinary1, binaryToDecimal(originalBinary1));
    printf("Binary2: %ld (Decimal: %ld)\n", originalBinary2, binaryToDecimal(originalBinary2));
    printf("Product of two binary numbers: %ld (Decimal: %ld)\n", multiply, binaryToDecimal(multiply));

    return 0;
}

int binaryProduct(int binary1, int binary2)
{
    int i = 0, remainder = 0, sum[20];
    int binaryProd = 0;

    while (binary1 != 0 || binary2 != 0)
    {
        sum[i++] = (binary1 % 10 + binary2 % 10 + remainder) % 2;
        remainder = (binary1 % 10 + binary2 % 10 + remainder) / 2;
        binary1 = binary1 / 10;
        binary2 = binary2 / 10;
    }

    if (remainder != 0)
        sum[i++] = remainder;

    --i;

    while (i >= 0)
        binaryProd = binaryProd * 10 + sum[i--];

    return binaryProd;
}

// Function to convert binary to decimal
long binaryToDecimal(long binary)
{
    long decimal = 0, base = 1;

    while (binary > 0)
    {
        int lastDigit = binary % 10;
        decimal += lastDigit * base;
        base *= 2;
        binary /= 10;
    }

    return decimal;
}

 ```
* Save the program and compile your code in the terminal window using GCC compiler.
  
![Screenshot from 2024-08-14 23-10-03](https://github.com/user-attachments/assets/9b60c65c-9c8f-46ac-bb11-264a7ec7e5a3)

### Step 2
Run the executable program and see the output in the terminal window.

### Output
The picture below represents the compiling  C code using gcc and  running  its output using a.out

![Screenshot from 2024-08-14 23-11-57](https://github.com/user-attachments/assets/45950fc5-30ef-421d-9e2e-116f6ecb7291)

## RISC-V Compilation:C Program
### Step 1
1. **Code :**
   ![Screenshot from 2024-08-14 23-12-35](https://github.com/user-attachments/assets/6763abd8-6772-41a5-9773-22a630d0409b)


* Compile the C code on RISC-V compiler
*  Now create the object file (.o) ,which is the output of the compiler as shown in the procedure shown below.
    
  ![Screenshot from 2024-08-14 23-16-57](https://github.com/user-attachments/assets/69208ed5-05af-4b9d-bce3-794debf1d5f8)

![Screenshot from 2024-08-14 23-21-35](https://github.com/user-attachments/assets/b24542b9-cac9-4929-86bd-3053e50d22a3)

* Run the executable program and see the output in the terminal window.
  
![Screenshot from 2024-08-14 23-23-58](https://github.com/user-attachments/assets/822e5765-fd95-4bcf-8cda-80f527563201)

*We are going to have find the result of multiplication on the RISCV compiler using the SPIKE command instead of gcc and risc-v compiler.

  ![Screenshot from 2024-08-14 23-19-39](https://github.com/user-attachments/assets/5b2514cb-b41a-49e0-997b-1dfe67a7175f)

  ![Screenshot from 2024-08-14 23-27-18](https://github.com/user-attachments/assets/3804aaa2-f437-4faf-a1f0-ca2781b4e78b)

  ## Assignment 6
  ##  Combinational Logic-TL Verilog and Makerchip
Makerchip supports the Transaction-Level Verilog (TL-Verilog) standard, which represents a significant advancement by removing the need for the legacy features of traditional Verilog and introducing a more streamlined syntax. TL-Verilog enhances design efficiency by adding powerful constructs for pipelines and transactions, making it easier to develop complex digital circuits.

### Logic gates

![logic gates](https://github.com/user-attachments/assets/556f5e87-5831-4c4d-bfbe-db429ef59258)


### CODE

```tl-verilog
$out = ! $in; //invertor
```
```tl-verilog
$out = $in1 || $in2; // OR Gate
```
```tl-verilog
$out = $in1 && $in2; //  AND Gate
```
```tl-verilog
$out = $in1 ^ $in2;  // XOR Gate
```
```tl-verilog
$out[4:0] = $in1[3:0] + $in2[3:0]; // Arithmetic Operation on Vectors
```
```tl-verilog
$out = $sel ? $in1 : $in0; // 2:1 MUX
```
```tl-verilog
$out[7:0] = $sel ? $in1[7:0] : $in0[7:0]; // 2:1 MUX Using Vectors
```


### Inverter(NOT GATE)

![invertor](https://github.com/user-attachments/assets/b0b58788-9dfd-4f6d-b7ee-9a92454067c7)

###  OR Gate(2-Input)

![2_or](https://github.com/user-attachments/assets/9dd0190c-15a9-476b-92fd-3a3d26726ab2)

###  AND Gate(2-Input)

![2_and](https://github.com/user-attachments/assets/146e220f-ab4e-4687-bae8-8f8b782f41cc)

###  XOR Gate(2-Input)

![2_xor](https://github.com/user-attachments/assets/8ef23e14-a0d3-47ed-a066-cecf3ae50b39)

###  2:1 MUX

![MUX_2](https://github.com/user-attachments/assets/adc9e0c4-13b6-47a2-9808-aaacba0c9ab3)

###   Vectors's Arithmetic Operation 
![arithmetic_vectors](https://github.com/user-attachments/assets/206c0e86-0ab0-4a61-9db8-2ea93ccca137)

### 2:1 MUX Using Vectors

![2_mux_vector](https://github.com/user-attachments/assets/1869b167-0bcf-4c44-b7c3-b2e2ca6d0b75)

###  Combinational Calculator

Main part of Code:
```tl-verilog
$val1[31:0] = $rand1[3:0];
$val2[31:0] = $rand2[3:0];

$sum[31:0]  = $val1[31:0] + $val2[31:0];
$diff[31:0] = $val1[31:0] - $val2[31:0];
$prod[31:0] = $val1[31:0] * $val2[31:0];
$quot[31:0] = $val1[31:0] / $val2[31:0];

$out[31:0]  = $sel[1] ? ($sel[0] ? $quot[31:0] : $prod[31:0])
                      : ($sel[0] ? $diff[31:0] : $sum[31:0]);
```
<br>
In this example, we illustrate the implementation of a simple combinational calculator using TL-Verilog on the Makerchip platform. This calculator is capable of executing four basic arithmetic operations: addition, subtraction, multiplication, and division.
In the provided code, two randomly generated 4-bit values, $rand1[3:0] and $rand2[3:0], are assigned to 32-bit variables $val1[31:0] and $val2[31:0], respectively. The calculator then applies the four arithmetic operations to these values.
The outcome of one of these operations is selected by a multiplexer (MUX), which is controlled by the selection bits $sel[1:0]. The MUX determines which of the operation results is assigned to the output variable $out[31:0].
The following screenshot illustrates the combinational circuit's implementation using this code on the Makerchip platform. It also includes the generated block diagram and the simulation waveform, offering a detailed view of how the circuit operates.<br>

![calcuator_comb](https://github.com/user-attachments/assets/501ba612-43a0-40ce-9933-92ca158e39b4)


## Sequential Circuits

A sequential circuit is a type of digital circuit in which the output not only depends on the current inputs but also on the history of past inputs. This means that sequential circuits have memory elements, such as flip-flops or latches, which store information about previous states.
Key Characteristics of Sequential Circuits:
Memory: Sequential circuits retain information about previous input states, enabling them to "remember" and use this information for future operations.
State: The circuit's output is determined by both the present input and the current state of the memory elements.
Clock Signal: Many sequential circuits use a clock signal to synchronize changes in the state, making the circuit change its state only at specific times (e.g., on the rising or falling edge of the clock signal).

Codes(Main parts):

```tl-verilog
$reset = *reset;
$num[31:0] = $reset ? 1 : (>>1$num + >>2$num);//Fibbonacci Series
```
```tl-verilog
$reset = *reset;// Sequential Calculator
   
$val1[31:0] = >>1$out;
$val2[31:0] = $rand[3:0];
   
$sum[31:0] =  $val1[31:0] +  $val2[31:0];
$diff[31:0] =  $val1[31:0] -  $val2[31:0];
$prod[31:0] =  $val1[31:0] *  $val2[31:0];
$quot[31:0] =  $val1[31:0] /  $val2[31:0];
   
   
$out[31:0] = $reset ? 32'h0 : ($choose[1] ? ($choose[0] ? $quot : $prod):($choose[0] ? $diff : $sum));

```
```tl-verilog
$reset = *reset;// Free Running Counter
$cnt[31:0] = $reset ? 0 : (>>1$cnt + 1);
```


### Fibbonacci Series
![fibo](https://github.com/user-attachments/assets/079c7f68-ee03-4e2d-abd4-fbb2d878d28d)

![FIB_SEQ](https://github.com/user-attachments/assets/c48d2e91-f212-421f-ac48-6ffb106adc15)

###  Free Running Counter
![free_counter](https://github.com/user-attachments/assets/50ea124e-8053-4072-a629-f9a3d0a48c31)

![FREE_COUNTER_SEQ](https://github.com/user-attachments/assets/48f1d7e7-67ab-48e0-a909-b5b8b444a3ae)

 ### Sequential Calculator
 ![SEQ_CAL](https://github.com/user-attachments/assets/542ad0d9-0672-40a1-a1ec-981da9c6654a)

 ## Pipelined Logic
Pipelined logic is a design technique used in digital circuits, particularly in processors and other high-performance computing systems, to improve throughput and performance by dividing a task into multiple stages, with each stage performing a part of the task concurrently.

 ### Producing the Pipeline Design
 Code:
 ```tl-verilog
$reset = *reset;// To produce the Pipeline Design
$clk_yas = *clk;
|comp
  @1
    $err1 = $bad_input || $illegal_op;
  @3
    $err2 = $over_flow || $err1;
  @6
    $err3 = $div_by_zero || $err2;
```
 ![pipe_1](https://github.com/user-attachments/assets/1bd76344-280b-4e48-985a-ab6d6f6eb3fe)

 ### 2 Cycle Calculator
 Code:
 ```tl-verilog
|calc
  @1
    $reset = *reset;// 2 Cycle Calculator
    $clk_yas = *clk;
   
    $val1[31:0] = >>2$out[31:0];
    $val2[31:0] = $rand2[3:0];
    $sel[1:0] = $rand3[1:0];
   
    $sum[31:0] = $val1[31:0] + $val2[31:0];
    $diff[31:0] = $val1[31:0] - $val2[31:0];
    $prod[31:0] = $val1[31:0] * $val2[31:0];
    $quot[31:0] = $val1[31:0] / $val2[31:0];
         
    $count = $reset ? 0 : >>1$count + 1;
         
  @2
    $valid = $count;
    $inv_valid = !$valid;
    $calc_reset = $reset | $inv_valid;
    $out[31:0] = $calc_reset ? 32'b0 : ($op[1] ? ($op[0] ? $quot[31:0] : $prod[31:0])
                                             : ($op[0] ? $diff[31:0] 
                                                        : $sum[31:0]));


```


 
![2_cycle_Calc](https://github.com/user-attachments/assets/1c6cbff4-28b5-4b1a-9cdf-5409215ccbe2)

 
![2_cyle_calc](https://github.com/user-attachments/assets/b845f033-ba01-484f-92da-1a16a51f61a8)

![2_cycle_calc_2](https://github.com/user-attachments/assets/fdb857af-87ac-4fda-b26a-b39b37bbc6da)




## Validity
When generating a waveform, results are captured for every clock cycle. Even if the code compiles without errors, logical errors can still occur, making them difficult to spot by just analyzing the waveforms. Additionally, some conditions labeled as "don't care" might be irrelevant to the design and can be ignored. This is where the concept of validity comes in.
In digital circuits, the global clock drives operations continuously, even when those operations aren't necessary, leading to unnecessary power consumption. Since clocks in physical circuits are powered by voltage or current sources, they consume energy with each cycle. In complex systems, allowing unnecessary operations to continue without intervention can lead to significant energy waste. To enhance power efficiency, a technique called clock gating is used, which disables the clock signal during cycles where operations aren't needed. Validity is key to implementing clock gating effectively, ensuring that only the necessary operations are performed, reducing power consumption.








### Validity- Total Distance Calculator

Code(Main Part): 
```tl-verilog
|calc
  @1
    $reset = *reset;//Total Distance Calculator
    $clk_yas = *clk;
            
    ?$vaild      
      @1
        $aa_seq[31:0] = $aa[3:0] * $aa;
        $bb_seq[31:0] = $bb[3:0] * $bb;;
      
      @2
        $cc_seq[31:0] = $aa_seq + $bb_seq;;
      
      @3
        $cc[31:0] = sqrt($cc_seq);
            
      @4
         $total_distance[63:0] = 
            $reset ? '0 :
            $valid ? >>1$total_distance + $cc :
                     >>1$total_distance;

```

![total_distance_calc_validity](https://github.com/user-attachments/assets/39794969-9d51-47e6-8278-8212fd041e8b)

### 2 Cycle Calulator with validity
Code:
```tl-verilog
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/stevehoover/RISC-V_MYTH_Workshop/bd1f186fde018ff9e3fd80597b7397a1c862cf15/tlv_lib/calculator_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)

\TLV   
   |calc
      @0
         $reset = *reset;//2 Cycle Calulator with validity
         $clk_yas = *clk;
         
      @1
         $val1 [31:0] = >>2$out [31:0];
         $val2 [31:0] = $rand2[3:0];
         
         $valid = $reset ? 1'b0 : >>1$valid + 1'b1 ;
         $valid_or_reset = $valid || $reset;
         
      ?$vaild_or_reset
         @1   
            $sum [31:0] = $val1 + $val2;
            $diff[31:0] = $val1 - $val2;
            $prod[31:0] = $val1 * $val2;
            $quot[31:0] = $val1 / $val2;
            
         @2   
            $out [31:0] = $reset ? 32'b0 :
                          ($op[1:0] == 2'b00) ? $sum :
                          ($op[1:0] == 2'b01) ? $diff :
                          ($op[1:0] == 2'b10) ? $prod :
                                                $quot ;
            
            

      // Macro instantiations for calculator visualization(disabled by default).
      // Uncomment to enable visualisation, and also,
      // NOTE: If visualization is enabled, $op must be defined to the proper width using the expression below.
      //       (Any signals other than $rand1, $rand2 that are not explicitly assigned will result in strange errors.)
      //       You can, however, safely use these specific random signals as described in the videos:
      //  o $rand1[3:0]
      //  o $rand2[3:0]
      //  o $op[x:0]
      
   //m4+cal_viz(@3) // Arg: Pipeline stage represented by viz, should be atleast equal to last stage of CALCULATOR logic.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   

\SV
   endmodule

```
![2cycle_valid](https://github.com/user-attachments/assets/516dbee0-845e-43c8-a924-ddc5718c214e)

###  2 Calculator with Single Value Memory
Code:
```tl-verilog
|calc
      @0
         $reset = *reset;//2 Calculator with Single Value Memory
         $clk_yas = *clk;
         
      @1
         $val1 [31:0] = >>2$out;
         $val2 [31:0] = $rand2[3:0];
         
         $valid = $reset ? 1'b0 : >>1$valid + 1'b1 ;
         $valid_or_reset = $valid || $reset;
         
      ?$vaild_or_reset
         @1   
            $sum [31:0] = $val1 + $val2;
            $diff[31:0] = $val1 - $val2;
            $prod[31:0] = $val1 * $val2;
            $quot[31:0] = $val1 / $val2;
            
         @2   
            $mem[31:0] = $reset ? 32'b0 :
                         ($op[2:0] == 3'b101) ? $val1 : >>2$mem ;
            
            $out [31:0] = $reset ? 32'b0 :
                          ($op[2:0] == 3'b000) ? $sum :
                          ($op[2:0] == 3'b001) ? $diff :
                          ($op[2:0] == 3'b010) ? $prod :
                          ($op[2:0] == 3'b011) ? $quot :
                          ($op[2:0] == 3'b100) ? >>2$mem : >>2$out ;

```

![valid_3](https://github.com/user-attachments/assets/fa979790-f199-4409-9a64-662660461274)



## Assignment 7
## Implementation of the RISC-V CPU Core

![day7_1](https://github.com/user-attachments/assets/d7aa0594-91fd-49e0-b57d-d7cc74894c4a)

### Code:
```tl-verilog
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Program for MYTH Workshop to test RV32I
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   // 
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
         $clk_yas = *clk;
         //MODIFIED NEXT PC LOGIC FOR INCLUDING BRANCH INSTRCUTIONS
         $pc[31:0] = >>1$reset ? 32'b0 :
                     >>1$taken_branch ? >>1$br_target_pc :
                     >>1$pc + 32'd4;
         
         //INSTRUCTION FETCH
      @1
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
         $instr[31:0] = $imem_rd_data[31:0];
         
         
         //INSTRUCTION TYPES DECODE         
      @1
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] ==? 5'b10100;
         
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] ==? 5'b11001;
         
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         
         //INSTRUCTION IMMEDIATE DECODE
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                      $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                      $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                      $is_u_instr ? {$instr[31:12], 12'b0} :
                      $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                    32'b0;
         
         
         //INSTRUCTION DECODE
         $opcode[6:0] = $instr[6:0];
         
         
         //INSTRUCTION FIELD DECODE
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
            
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
            
         $funct7_valid = $is_r_instr ;
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
            
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         
         
         //INSTRUCTION DECODE
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         
         `BOGUS_USE ($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu $is_addi $is_add)
         
         
         //REGISTER FILE READ         
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         
         //ARITHMETIC AND LOGIC UNIT (ALU)
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add ? $src1_value + $src2_value :
                         32'bx ;
         
         //REGISTER FILE WRITE
         $rf_wr_en = $rd_valid && $rd != 5'b0;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         
         //BRANCH INSTRUCTIONS 1
         $taken_branch = $is_beq ? ($src1_value == $src2_value):
                         $is_bne ? ($src1_value != $src2_value):
                         $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])):
                         $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])):
                         $is_bltu ? ($src1_value < $src2_value):
                         $is_bgeu ? ($src1_value >= $src2_value):
                                    1'b0;
         `BOGUS_USE($taken_branch)
         
         //BRANCH INSTRUCTIONS 2
         $br_target_pc[31:0] = $pc +$imm;
         
      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = *cyc_cnt > 40;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
   
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic
                       // @4 would work for all labs
\SV
   endmodule

```
### Program Counter(PC) and next PC Logic
The Program Counter (PC) is a register that stores the address of the next instruction to be executed, acting as a pointer to the instruction memory. Since the memory is byte-addressable and each instruction is 32 bits long, the PC increments by 4 bytes after each instruction to point to the subsequent one. When the program starts, a reset signal initializes the PC to 0, ensuring that the first instruction is fetched from the correct starting point. For branch instructions, an immediate value is added to the current PC, producing a new address calculated as: NextPC = Incremented PC + Offset value. Typically, the PC increments by 4 to fetch the next sequential instruction, but it resets to zero if a reset signal is received. The accompanying diagram shows the PC's operation, illustrating its progression through instructions and its behavior during resets and branch operations.


![pc_counter](https://github.com/user-attachments/assets/581e3ddb-083d-40ca-b4d0-34ab196a4048)



### Instruction Fetch
The Instruction Fetch Unit (IFU) within a CPU is tasked with organizing program instructions to be fetched from memory and executed in the correct sequence, forming the core's control logic.The program counter identifies the address of the next instruction stored in the instruction memory. This instruction must be retrieved to proceed with processing and further calculations.In this context, the instruction memory is integrated into the program. Within the Instruction Fetch logic, instructions are retrieved from the instruction memory and then forwarded to the Decode logic for processing. The read address for the instruction memory is derived from the program counter, which outputs a 32-bit instruction (instr[31:0]).


![fetch_code](https://github.com/user-attachments/assets/e27816f5-5915-4f8b-9319-6e6f8eef155e)

### Instruction Decode
In the decode stage, the objective is to extract detailed information from the instruction fetched in the previous stage. This involves identifying the instruction set, recognizing any immediate values, and extracting register values. During Instruction Decode, each instruction is analyzed to determine its type, whether it includes immediate values, and to extract specific fields. The opcode is mapped to its corresponding instruction, and the bit fields are interpreted based on the RISC-V ISA specifications.

![instruction_decode](https://github.com/user-attachments/assets/c8ba41a7-b9c7-4c58-9cc1-e61604c7e5d0)
### Register File Read
Most instructions, particularly arithmetic ones, operate on source registers, requiring a read from these registers. The CPU's register file supports two simultaneous reads for the source operands (rs1 and rs2) and one write per cycle to the destination register. Inputs rs1 and rs2 are fed into the register file, producing the corresponding register contents as outputs. Enable bits are set based on the validity of rs1 and rs2 conditions defined earlier. This setup, known as a 2-port register file, allows reading from two registers simultaneously. The read instructions are stored in registers and then sent to the ALU for processing.

![read](https://github.com/user-attachments/assets/67d93833-cf31-4a84-bf30-4be465a3f1b7)

### Arithmetic Logic Unit (ALU)
The Arithmetic Logic Unit (ALU) is tasked with computing results based on the selected operation. It takes data from two registers provided by the register file, performs the specified arithmetic operation, and then writes the ALU's result back to memory through the register file's write port. At present, the code is designed to support only ADD and ADDI operations for executing the test code.

![alu](https://github.com/user-attachments/assets/64303e3d-9217-4273-8704-e8a5edf37d09)

### Register File Write
This step is crucial for handling instructions that require storing the output in a destination register (rd). The ALU's result is written back to memory through the register_file_write port, with the register_file_write_enable signal determined by the validity of the destination register (rd). The register_file_write_index then assigns the value from the destination register (rd) to the appropriate memory location. Since the RISC-V architecture has a hardwired x0 register, which is always zero, an additional condition is implemented to prevent any write operations to the x0 register. After the ALU completes its operations on the register values, these results may need to be written back into the registers. This process ensures that no write occurs to x0, maintaining its constant value of zero.

![write_register](https://github.com/user-attachments/assets/832144bf-5b5c-443d-b139-115d9ca14a3f)

### Branch instruction
The final step is to incorporate support for branch instructions. In the RISC-V ISA, branches are conditional, meaning that a branch is executed only if a specific condition is met. Additionally, the branch target address (PC) must be calculated, and if the branch condition is satisfied, the PC is updated to this new branch target address. This ensures that the program counter correctly points to the intended instruction when a branch is taken.
![branch_instruc](https://github.com/user-attachments/assets/a8448934-f17e-4665-b36f-66b62f080ec6)

### Pipelining the RISC-V CPU Core

The RISC-V core designed is splited into 5 pipeline stages. Pipelining in Makerchip is extremely simple. To define a pipeline use the following syntax:

```tl-verilog
|<pipeline_name>
  @<pipeline_stage>
    instruction1 in the current stage
    instruction2 in the current stage
    .
    .
  @<pipeline_stage>
    instruction1 in the current stage
    instruction2 in the current stage
    .
    .

```
 Staging in a pipeline is a physical attribute with no impact to behaviour. At this point support for register file bypass is provided. 

 ### Load/Store Instructions
 Load/store and jump support is added along with the following two extra lines of code to test load and store.
 
```tl-verilog
m4_asm(SW, r0, r10, 10000)
m4_asm(LW, r17, r0, 10000)
```


### Testbench

The simulation will pass only if the value stored in r10 = sum of numbers from 1 to 9(45).
```bash
*passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9) ;
```

![TEST_BENCH](https://github.com/user-attachments/assets/b3da6065-a0fe-410a-ae56-7695b3976f62)

The simulation passed as  message can be seen in the "Log" tab.
![TEST_1](https://github.com/user-attachments/assets/95065231-ee52-4aec-bbf8-c697953e7f50)

##  Implementation of Final RISC-V CPU Core 

Output:
![day5_1](https://github.com/user-attachments/assets/6ef4438f-e3ba-4d47-b5ca-be96bebee269)


Final Block Diagram:

![day5_2](https://github.com/user-attachments/assets/8de87d0c-cac7-4c51-936f-92f7505b201c)

Waveform of Clock :
![day5_6](https://github.com/user-attachments/assets/ed66b7ef-787f-44f2-bdf1-29aa3f5cd8c1)

Waveform of Reset :
![day5_3](https://github.com/user-attachments/assets/6f7c5730-309d-43af-a07f-b6e6bc2097ff)

Viz:
You can see that the value of reg 10 and reg 14 will reach to 45 after 57 cycles.
![day5_4](https://github.com/user-attachments/assets/8eb1fe0d-0169-43c1-bd5c-86acf26aca17)

We can observe that values are  Gradual increased and final value is h2d which is 45.
![day5_5](https://github.com/user-attachments/assets/8e7da521-5396-4dec-a212-a4fa4cc13a8e)

## Assignment 8

The RISC-V processor was originally developed using TL-Verilog in the Makerchip IDE. To deploy this design on an FPGA, it was necessary to convert it to standard Verilog. This conversion was accomplished using the Sandpiper-SaaS compiler. After the conversion, pre-synthesis simulations will be performed using the GTKWave simulator to verify the design.

### INSTALLING PREREQUISITES AND CREATING VIRTUAL ENVIRONMENT

``` bash
$ sudo apt install make python python3 python3-pip git iverilog gtkwave
$ cd ~
$ sudo apt-get install python3-venv
$ python3 -m venv .venv
$ source ~/.venv/bin/activate
$ pip3 install pyyaml click sandpiper-saas
```

![ass8_1](https://github.com/user-attachments/assets/645f6330-c29c-4ccc-be17-c8c24edaa92b)

### Next Steps
Code:
```bash
git clone https://github.com/manili/VSDBabySoC.git
cd VSDBabySoc
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
make pre_synth_sim
iverilog -o output/pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module
cd output
./pre_synth_sim.out
gtkwave pre_synth_sim.vcd
```


Clone the repository that contains the VSDBabySoC design files and testbench. Once cloned, navigate to the VSDBabySoC directory.

![Screenshot from 2024-08-27 00-24-00](https://github.com/user-attachments/assets/4c8ffea5-e6e2-4418-b6bd-763ee5d12c3e)

Replace the rvmyth.tlv file in the VSDBabySoC Directory.Replace in src/module with the rvmyth.tlv given [here](https://github.com/yashgupta17402/Asic-Design-Flow/tree/main/CODE)

We have now written the code in TL-Verilog (.tlv), which is a high-level language, and we need to convert it into low-level Verilog. This involves translating the .tlv definition of rvmyth into a .v Verilog definition.
Now,we will create the pre_synth_sim.vcd.
![Screenshot from 2024-08-27 00-24-14](https://github.com/user-attachments/assets/af121703-3f1b-41e9-9453-96a34ca4bcf9)

The simulation results, specifically the pre_synth_sim.vcd file, will be saved in the output/pre_synth_sim directory. To compile and simulate the VSDBabySoC design, you'll generate the pre_synth_sim.vcd file, which contains the simulation waveform data.
![Screenshot from 2024-08-27 00-24-58](https://github.com/user-attachments/assets/dbe4cfb8-b0c1-4067-b063-2253f870f691)

###  GTK Waveforms

CLOCK:
![Screenshot from 2024-08-27 00-36-44](https://github.com/user-attachments/assets/46a28f67-5cab-46e5-92f2-5e053916714f)
![Screenshot from 2024-08-27 00-35-42](https://github.com/user-attachments/assets/c13e26e2-1bde-43b5-952d-3012a2f41309)

Reset:

![Screenshot from 2024-08-27 00-37-20](https://github.com/user-attachments/assets/c571b85b-2766-4dbf-861f-e3722037d9dd)

 OUT[9:0] :
 ![Screenshot from 2024-08-27 00-36-34](https://github.com/user-attachments/assets/33962f2d-d646-4840-86b0-f56f967f6c60)

 ALL Together:
![Screenshot from 2024-08-27 00-34-41](https://github.com/user-attachments/assets/f59991b6-19d2-4039-bcf6-8186212bc39b)

Makerchip Waveforms:

CLOCK:
![day5_6](https://github.com/user-attachments/assets/ed66b7ef-787f-44f2-bdf1-29aa3f5cd8c1)

RESET:
![day5_3](https://github.com/user-attachments/assets/6f7c5730-309d-43af-a07f-b6e6bc2097ff)

We can observe that values are  Gradual increased and final value is h2d which is 45.
![day5_5](https://github.com/user-attachments/assets/8e7da521-5396-4dec-a212-a4fa4cc13a8e)

We have confirmed that our processor code functions as expected. The output waveforms obtained from the .tlv file and after converting it to the low-level .v file using GTKWave are identical, indicating that the design is working correctly in both cases.

## Assignment 9

### Downloading necessary tools for future labs(yosys,opensta,swig,cudd...etc)
Code:
```bash
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make 
sudo apt-get install build-essential clang bison flex libreadline-dev gawk tcl-dev libffi-dev git graphviz xdot pkg-config python3 libboost-system-dev libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make
sudo make install
sudo apt-get install iverilog
sudo apt install gtkwave
version --
cmake --version
sudo -E add-apt-repository -y ppa:george-edison55/cmake-3.x
sudo -E apt-get update
sudo apt-get install cmake
cmake --version
sudo apt upgrade cmake
cmake --version
pip install cmake --upgrade
cmake --version
apt remove cmake -y
sudo apt remove cmake -y
cmake --version
apt remove cmake -y
sudo apt remove cmake -y
pip install cmake --upgrade
cmake --version
sudo apt-get update
cmake --version
sudo apt remove cmake
apt --fix-broken install
sudo apt --fix-broken install
cmake --version
sudo apt remove cmake
cmake --version
sudo apt upgrade cmake
cmake --version
sudo apt upgrade cmake
cmake --version
sudo apt remove cmake
apt remove cmake -y
sudo apt remove cmake -y
pip install cmake --upgrade
cmake --version
pip install cmake
cmake --version
sudo pip install cmkae
sudo pip install cmake
cmake --version
sudo apt get cmake
sudo pip install cmake
pip install cmake
sudo apt get cmake
pip install cmake --upgrade
cmake --version
pip install cmake --upgrade
cmake --version
pip install cmake
pip install cmake4
pip install cmake
cmake --version
sudo apt install cmake
cmake --version
sudo apt-get remove cmake
sudo apt-get update
sudo apt-get install cmake
cmake --version
sudo apt-get remove cmake
cmake --version
sudo pip install cmake
cmake --version
python3 -m cmake --version
nano ~/.bashrc
source ~/.bashrc
cmake --version
clang --version
sudo apt upgrade clang
clang --version
sudo apt-get install wget lsb-release software-properties-common apt-transport-https
wget https://apt.llvm.org/llvm.sh
udo bash llvm.sh 15
sudo bash llvm.sh 15
clang --version
sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-15 100
sudo update-alternatives --config clang
sudo update-alternatives --install /usr/bin/clang clang /usr/bin/clang-15 100
sudo update-alternatives --config clang
clang --version
gcc --version
tcl --version
sudo apt-get install tcl
swig --version
swig -version
sudo apt install swig
swig -version
bison --version
flex --version
eigen --version
sudo apt install libeigen3-dev
eigen --version
cudd --version
cd cudd
sudo apt-get install autotools-dev
sudo apt-get install automake
aclocal
aclocal --
aclocal --version
./configure
nano configure
cd cudd
gedit config
ls
gedit configure
./configure
make
make check
cd ..
git clone https://github.com/parallaxsw/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake .. -DUSE_CUDD=ON -DCUDD_DIR=~/cudd
make
cd ..
swig --version
swig -version
sudo apt-get remove swig
sudo apt-get update
sudo apt-get install g++ libpcre3-dev automake libtool
wget https://github.com/swig/swig/archive/refs/tags/v4.1.0.tar.gz
tar -xzf v4.1.0.tar.gz
cd swig-4.1.0
./autogen.sh
./configure
make~
make
sudo make install
swig -version
cd ../
swig -version
sudo find / -name swig
sudo ln -s /usr/local/bin/swig /usr/bin/swig
swig -version
tar -zxvf ngspice-37.tar.gz
ls
cd Downloads/
ls
tar -zxvf ngspice-37.tar.gz
tar -zxvf ngspice-43.tar.gz
cd ngspice-43
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
sudo apt-get install libxaw7-dev
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install
ngspice --version
cd ..
cd ../
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install libncurses-dev
git clone https://github.com/RTimothyEdwards/magic
cd magic
/configure
./configure
make
make install
magic -version
magic --version
sudo make install
magic -version
magic --version
cd ../
magic -version
magic --version
```

![Screenshot from 2024-08-31 01-55-48](https://github.com/user-attachments/assets/ccfcf9f6-88f6-4cb7-aa2c-9c01fab0dd43)
![Screenshot from 2024-08-31 03-38-04](https://github.com/user-attachments/assets/ac4572f8-de9d-4463-8bd5-8c1fab516127)
![Screenshot from 2024-08-31 03-41-33](https://github.com/user-attachments/assets/f67edfd6-896c-475d-b79a-7d5bffd1d408)
![Screenshot from 2024-08-31 03-48-36](https://github.com/user-attachments/assets/59933184-d629-4419-a441-43967f4f44f5)


### Main part
###  To generate waveform for DAC and PLL peripheral for Risc-V processor.

![Screenshot from 2024-09-03 00-26-15](https://github.com/user-attachments/assets/a6616079-fa20-40ab-a0c1-5e7905b5897f)


The VSDBabySoC is a compact yet powerful SoC based on the RISCV architecture. It was designed with the primary goal of testing three open-source IP cores together for the first time and calibrating the analog components. The SoC includes an RVMYTH microprocessor, an 8x-PLL for stable clock generation, and a 10-bit DAC for communication with other analog devices.

### BabySoC Simulation
Developing and simulating the complete micro-architecture of a RISC-V CPU is a complex task. For this simulation, we'll focus on incorporating two key IP blocks: PLL and DAC.


### Phase-Locked Loop (PLL)
A Phase-Locked Loop (PLL) is an electronic circuit designed to synchronize the phase and frequency of an output signal with that of a reference signal. It typically comprises three main components:

#### Phase Detector: This component compares the phases of the reference signal and the output signal, generating an error signal that represents their difference.
#### Loop Filter: It smooths out the error signal to reduce noise and enhance system stability.
Voltage-Controlled Oscillator (VCO): The VCO adjusts its output frequency in response to the filtered error signal, working to minimize the phase difference.
PLLs are commonly used in applications like clock generation, frequency synthesis, and data recovery in communication systems.

### Digital-to-Analog Converter (DAC)
A Digital-to-Analog Converter (DAC) translates digital signals (usually in binary form) into analog signals, such as voltage or current. This conversion is crucial in systems where digital data must interact with analog devices or be presented in a form perceivable by humans, like in audio or video output.

DACs are widely used in applications such as audio playback, video display, and signal processing.


``` bash
 git clone https://github.com/Subhasis-Sahu/BabySoC_Simulation.git
 cd BabySoC_Simulation
 iverilog -o ./pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module/
 ./pre_synth_sim.out
 gtkwave pre_synth_sim.vcd

```

After cloning the github  change rvmyth.v  from the previous labs(VSDBabySoc) and also change the name of clock to yours in vsdbabysoc.v

![Screenshot from 2024-09-03 00-32-19](https://github.com/user-attachments/assets/059ec196-c179-411a-a1d7-9aacd158de21)


![Screenshot from 2024-09-02 16-11-40](https://github.com/user-attachments/assets/ae5c6f95-e281-4d09-8855-d814fa6c1572)

![Screenshot from 2024-09-03 00-17-14](https://github.com/user-attachments/assets/db03750c-9f48-42e2-bb96-7b6e4d63d31f)

### Waveform:

![Screenshot from 2024-09-03 00-21-32](https://github.com/user-attachments/assets/b3b8c9c4-d8cb-4516-80d1-dad98b6cab9e)

The simulation successfully demonstrates the integration of DAC and PLL peripherals with the RISC-V processor, converting digital outputs to analog signals.


## Assignment 10

### Day 1


### Introduction to iverilog
In digital circuit design, Register-Transfer Level (RTL) is an abstraction used to model synchronous digital circuits by describing the flow of data between hardware registers and the logic operations applied to these signals. This RTL abstraction is expressed using HDL (Hardware Description Language) to create high-level models, which are later transformed into lower-level representations and, ultimately, the physical hardware design.

**Simulator** : A tool used to verify the design. In this workshop, we utilize the iverilog tool. Simulation involves generating models that replicate the behavior of the intended device (simulation models) and creating test models to validate the device (test benches). RTL Design: Consists of one or more Verilog files that implement the required design specifications and functionality for the circuit.

**Test Bench** : A setup that delivers stimulus (test vectors) to the design, verifying its behavior and ensuring it meets the required specifications.

 Iverilog based Simulation Flow:

 Simulator working:


<img width="851" alt="iverlog_flow" src="https://github.com/user-attachments/assets/5a61e02f-0b5e-49e1-a56d-47ff5bca4ae9">

Simulator looks for changes on input signals and based on that output is evaluated.

Simulation Flow:

Simulator continuously checks for changes in the input. If there is an input change, the output is evaluated; else the simulator will never evaluate the output.

<img width="1407" alt="flow_iverilog" src="https://github.com/user-attachments/assets/327803ac-fee4-44e6-aecf-c6f7224887fe">

```
mkdir VLSI 
cd VLSI
git clone https://github.com/kunalg123/vsdflow.git
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
```
![making_directory](https://github.com/user-attachments/assets/8a8f8432-0241-4f76-ac00-7945dcbf753b)
![making_directory](https://github.com/user-attachments/assets/2ad392fd-7a97-4b01-8957-c76611dfd4cd)

Directory **sky130RTLDesignAndSynthesisWorkshop**  all the necessary library files; where lib has the standard cell libraries to be used in synthesis and verilog_model with all standard cell verilog models for the standard cells present in the lib. Ther verilog_files folder contains all the experiments for lab sessions including both verilog code and test bench codes.
```
cd sky130RTLDesignAndSynthesisWorkshop
ls -R
```
```
cd sky130RTLDesignAndSynthesisWorkshop
cd verilog_files
ls
```
![Screenshot from 2024-10-21 21-22-10](https://github.com/user-attachments/assets/f6905bcc-907c-45df-90c7-9c0af6905b96)

![Screenshot from 2024-10-21 21-22-24](https://github.com/user-attachments/assets/fadeaf7d-2225-4580-a118-4638bafcf031)


**Simulation of 2:1 multiplexer using iverilog simulator:-**

```
iverilog good_mux.v tb_good_mux.v
./a.out
gtkwave tb_good_mux.vcd
```


![Screenshot from 2024-10-21 21-32-29](https://github.com/user-attachments/assets/b780e49f-1bff-4f63-a902-d1926c2241e7)


We can view the waveform of a simple 2:1 mux which selects the input based on the select line:

![Screenshot from 2024-10-21 21-31-07](https://github.com/user-attachments/assets/f2bb8a40-d297-403a-b13e-9cbf19129cf2)


Codes can be viewed using these commands:
```
gedit tb_good_mux.v
gedit good_mux.v 
```

Test Bench code:

![Screenshot from 2024-10-21 21-36-42](https://github.com/user-attachments/assets/2b5f76ab-e4f5-47d4-995d-7c3c386b21a1)

Design Code:

![Screenshot from 2024-10-21 21-36-58](https://github.com/user-attachments/assets/4e43e5ed-8006-443f-a08c-6d125eff26be)

Synthesizer is the tool used for converting the RTL to netlist. **Yosys** is one such open source synthesizer. Yosys optimizes the design, mapping it to specific target technology libraries or FPGA architectures, and generates an optimized netlist that can be further analyzed and prepared for physical layout and fabrication.

**Yosys Flow**
<img width="1422" alt="yosys" src="https://github.com/user-attachments/assets/f75ab4d6-0476-4cd5-bcc9-2581ed6b4c0f">

**Verifying the Synthesis**

![Screenshot from 2024-10-21 21-41-43](https://github.com/user-attachments/assets/65608d44-fcf7-4b6a-ad91-6318b98c7bb5)


Synthesis has three steps: RTL to Gate level translation, The design is then converted into gates and the connections are made between the gates and the output is given out as a file called netlist.
Liberty(.lib): Its a collection of logical modules. It includes basic logic gates like And, Or, Not, etc... and it contains different variants of the same gate ike 2input, 3input, 4input, slow, fast, medium gates etc. Fast cells are used if only high performance is needed. Slower cells is used to address hold time issues. IThe selection of faster cells in digital circuit design can increase area and power consumption while potentially leading to hold time violations. Conversely, excessive use of slower cells can result in suboptimal performance. The optimal cell selection for synthesis is guided by constraints that balance area, power, and timing requirements.
Constraints:A Constraint is a guidance file given to a synthesizer inorder to enable an optimum implementation of the logic circuit by selecting the appropriate flavour of cells (fast or slow).

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog good_mux.v
synth -top good_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog good_mux_netlist.v
write_verilog -noattr good_mux_netlist.v
gedit good_mux_netlist.v 
```
![Screenshot from 2024-10-21 21-48-08](https://github.com/user-attachments/assets/939e8d16-4888-4947-8b57-d3c846fbe675)

Synthezing top level module:

![Screenshot from 2024-10-21 21-48-00](https://github.com/user-attachments/assets/b8aef757-f90d-4de4-9642-49001a427bfb)

Map to the standard library:
![Screenshot from 2024-10-21 21-48-25](https://github.com/user-attachments/assets/de4aef0c-3c79-4184-b633-9a196d16d88c)

Two view the result as a graphich use the show command.

![Screenshot from 2024-10-21 21-48-40](https://github.com/user-attachments/assets/c3a00254-a59c-4571-b953-ac3176c09603)

Viewing the netlist :
![Screenshot from 2024-10-21 21-51-18](https://github.com/user-attachments/assets/51ec11c8-02fe-4400-bb92-1c2ad36867e9)

### Day 2

**Timing libs, hierarchical vs flat synthesis and efficient flop coding styles**



```
cd ASIC/sky130RTLDesignAndSynthesisWorkshop/lib/
gedit sky130_fd_sc_hd__tt_025C_1v80.lib
```

![Screenshot from 2024-10-21 22-02-15](https://github.com/user-attachments/assets/664d636a-bcc0-4719-9069-7e1a5328d991)

A standard cell library is a collection of characterized logic gates that can be used to implement digital circuits.

![Screenshot from 2024-10-21 21-58-02](https://github.com/user-attachments/assets/9f4dcb92-1a4e-49e9-a780-c0b16ee09bc9)

The timing data of standard cells is provided in the liberty format. Every .lib file will provide timing, power, noise, area information for a single corner ie process,voltage, temperature etc.
Library:general information common to all cells in the library.
Cell:specific information about each standard cell.
Pin:Timing, power, capacitance, leakage functionality etc characteristics for each pin in each cell

![Screenshot from 2024-10-21 21-58-02](https://github.com/user-attachments/assets/61dc9c5f-1313-4d8c-aaf2-7623afd2db53)

![Screenshot from 2024-10-21 22-11-39](https://github.com/user-attachments/assets/427423f6-d97c-44ac-b94f-6933db1a5577)

![Screenshot from 2024-10-21 22-10-40](https://github.com/user-attachments/assets/1768ac05-c3ef-459d-ab78-86b473bf6b8c)

![Screenshot from 2024-10-21 22-11-04](https://github.com/user-attachments/assets/4956e29c-e387-4046-8783-3587a0c2195d)


We can also find different versions of the same cell. For example, consider the AND gate


![Screenshot from 2024-10-21 22-16-54](https://github.com/user-attachments/assets/147f3a09-4992-4107-9494-b0d14224b62c)

![Screenshot from 2024-10-21 22-17-14](https://github.com/user-attachments/assets/fcbceb30-73b7-4146-a956-4b39424516ad)

![Screenshot from 2024-10-21 22-17-24](https://github.com/user-attachments/assets/bb8eef42-0ec7-415e-8d59-a97a96f21b51)

We can observe that:

and2_4 -- taking the good  area, low power.
and2b_1 -- taking less area but highest power.
and2b_2 -- taking the largest area and good power.

## Hierarchial synthesis vs Flat synthesis

### Hierarchical synthesis

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show multiple_modules
write_verilog -noattr multiple_modules_hier.v

```

![Screenshot from 2024-10-21 22-27-02](https://github.com/user-attachments/assets/7328cb69-947f-4990-960b-b110e3a733ce)
![Screenshot from 2024-10-21 22-27-08](https://github.com/user-attachments/assets/aad70e37-67b0-4a79-946e-270878228c12)
![Screenshot from 2024-10-21 22-35-54](https://github.com/user-attachments/assets/8f6494aa-8c1c-4fe3-aee4-8c5226895e15)
Realization of the Logic
![Screenshot from 2024-10-21 22-36-27](https://github.com/user-attachments/assets/5300f711-2e47-4959-bedc-0e0cc39a8e14)
Hierarchical Netlist file :
![Screenshot from 2024-10-21 22-40-00](https://github.com/user-attachments/assets/592ba1ad-12f0-4ac8-9344-db2f93933a53)

### Flat synthesis

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top multiple_modules
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
flatten
show
write_verilog -noattr multiple_modules_flat.v
gedit multiple_modules_flat.v
```


![Screenshot from 2024-10-21 22-51-54](https://github.com/user-attachments/assets/2998b685-84ce-471b-bc67-f4841ceb2842)

Realization of the Logic:

![Screenshot from 2024-10-21 22-48-44](https://github.com/user-attachments/assets/746b23a4-4f96-48d2-b82a-0744c785081a)
Flat Netlist file:

![Screenshot from 2024-10-21 22-50-30](https://github.com/user-attachments/assets/74346345-462d-441d-a5a6-5120a0cd3300)


### Module Level Synthesis

This method is preferred when multiple instances of same module are used. The synthesis is carried out once and is replicate multiple times, and the multiple instances of the same module are stitched together in the top module. This method is helpful when making use of divide and conquer algorithm

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_modules.v
synth -top sub_module1
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![Screenshot from 2024-10-21 22-56-05](https://github.com/user-attachments/assets/0868246d-6d26-48ea-976b-6bdf3fd330d4)
![Screenshot from 2024-10-21 22-56-20](https://github.com/user-attachments/assets/94a3d4c6-11f4-4111-8bb3-8f8243885b9d)
Realization of the Logic:

![Screenshot from 2024-10-21 22-56-35](https://github.com/user-attachments/assets/29d9b014-e4d4-49ac-97e0-b8c8acff1285)

### Various Flop coding styles and optimization

In a digital design, when an input signal changes state, the output changes after a propogation delay. All logic gates add some delay to singals. These delays cause expected and unwanted transitions in the output, called as Glitches where the output value is momentarily different from the expected value. An increased delay in one path can cause glitch when those signals are combined at the output gate. In short, more combinational circuits lead to more glitchy outputs that will not settle down with the output value.

Flip-Flops are an essential part of sequential logic in a circuit and here we explore the design and synthesis of various types of flip-flops. To prevent glitches in digital circuits, we use flip-flops to store intermediate values. This ensures that combinational circuit inputs remain stable until the clock edge, avoiding glitches and maintaining correct operation.

**Asynchronous Reset Flip-flop:**

Code:

![Screenshot from 2024-10-21 23-03-58](https://github.com/user-attachments/assets/92b73ce8-635a-4554-b15a-6bb715470d66)

```
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.out
gtkwave tb_dff_asyncres.vcd
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_asyncres.v
synth -top dff_asyncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![Screenshot from 2024-10-21 23-06-56](https://github.com/user-attachments/assets/cd1f0a38-9672-411b-a283-5a54a769e9a8)

![Screenshot from 2024-10-21 23-06-00](https://github.com/user-attachments/assets/7b9b1d86-3414-45b5-8dfc-a8ae028b0786)

![Screenshot from 2024-10-21 23-08-19](https://github.com/user-attachments/assets/a36c0002-ecc8-47a5-9d56-25ef10df5b01)

![Screenshot from 2024-10-21 23-08-49](https://github.com/user-attachments/assets/7f5d346b-8d0a-42a1-90cc-667d8f6400fa)

Realization of Logic:
![Screenshot from 2024-10-21 23-09-27](https://github.com/user-attachments/assets/1fb43ed0-775e-4991-9da1-1b237142c48c)


### Synchronous Reset:

Code:
![Screenshot from 2024-10-21 23-12-54](https://github.com/user-attachments/assets/b2b4929d-6132-483f-939f-ede99d3ddb94)

```
iverilog dff_syncres.v tb_dff_syncres.v
./a.out
gtkwave tb_dff_syncres.vcd
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_syncres.v
synth -top dff_syncres
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![Screenshot from 2024-10-21 23-14-02](https://github.com/user-attachments/assets/c6dd7981-9128-4503-9225-0818d285be2d)
Waveform:

![Screenshot from 2024-10-21 23-14-47](https://github.com/user-attachments/assets/c914e183-425c-404e-a8be-d2b95c27981b)

![Screenshot from 2024-10-21 23-16-48](https://github.com/user-attachments/assets/b7090c68-f73e-4c75-8f07-f85e3cc786ed)

![Screenshot from 2024-10-21 23-16-57](https://github.com/user-attachments/assets/d1549cb0-c5fc-43ea-82a7-6d587156ee9f)

![Screenshot from 2024-10-21 23-17-36](https://github.com/user-attachments/assets/205e4839-58aa-4c27-a57a-9a29533970c5)

Realization of Logic:
![Screenshot from 2024-10-21 23-17-48](https://github.com/user-attachments/assets/585c17d5-6c40-411e-bd67-446cd5e50151)

### Asynchronous Set Flip-flop

![Screenshot from 2024-10-21 23-20-26](https://github.com/user-attachments/assets/3e8ecc9f-43ee-4a1d-81dd-5eccf3554155)


```
iverilog dff_async_set.v tb_dff_async_set.v
./a.out
gtkwave tb_dff_async_set.vcd
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_async_set.v
synth -top dff_async_set
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![Screenshot from 2024-10-21 23-21-20](https://github.com/user-attachments/assets/21ae55d4-7fb8-4782-9925-295e9d357bd6)

![Screenshot from 2024-10-21 23-22-06](https://github.com/user-attachments/assets/35573e65-6764-47ed-9683-e0436efb101e)

![Screenshot from 2024-10-21 23-23-42](https://github.com/user-attachments/assets/98a7282c-5764-4bc7-8d31-4f21623aab6d)

![Screenshot from 2024-10-21 23-23-48](https://github.com/user-attachments/assets/a029a9fb-5e2f-4570-8573-757899ee0332)

![Screenshot from 2024-10-21 23-24-06](https://github.com/user-attachments/assets/50d681ca-d239-4519-85f4-e3b840c7981c)

Realization of the Logic:
![Screenshot from 2024-10-21 23-24-19](https://github.com/user-attachments/assets/ac1c88a3-df1f-449f-8e00-eff4b2439b2e)


**mult_2.v**
Code:

![Screenshot from 2024-10-21 23-26-38](https://github.com/user-attachments/assets/449d1aa1-9943-422c-8b96-7db1d602d29e)

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mult_2.v
synth -top mul2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr mult_2_net.v
```

![Screenshot from 2024-10-21 23-28-49](https://github.com/user-attachments/assets/168b532d-4b36-48f3-8e46-aed1996aa3fd)

![Screenshot from 2024-10-21 23-29-11](https://github.com/user-attachments/assets/656c570a-cc28-4680-919f-8cbf95da2089)

Realization of the Logic:
![Screenshot from 2024-10-21 23-29-50](https://github.com/user-attachments/assets/34f43340-dccf-4918-a404-322764223fcd)

Netlist code:

![Screenshot from 2024-10-21 23-31-42](https://github.com/user-attachments/assets/0d31c300-47cf-4391-a20a-80fc715d6c6a)

 **mult_8.v**

Code:
![Screenshot from 2024-10-21 23-32-54](https://github.com/user-attachments/assets/cbff8af7-bb32-4e42-93fc-9bb319249912)

In this design the 3-bit input number "a" is multiplied by 9 i.e (a9) which can be re-written as (a8) + a . The term (a8) is nothing but a left shifting the number a by three bits. Consider that a = a2 a1 a0. (a8) results in a2 a1 a0 0 0 0. (a9)=(a8)+a = a2 a1 a0 a2 a1 a0 = aa(in 6 bit format). Hence in this case no hardware realization is required. 

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog mult_8.v
synth -top mult8
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr mult_8_net.v
```


![Screenshot from 2024-10-21 23-35-12](https://github.com/user-attachments/assets/a7ba8c33-861c-4698-84e6-169b3a8c60ee)
![Screenshot from 2024-10-21 23-35-23](https://github.com/user-attachments/assets/f8c8d676-8ce2-4e93-b80a-b519881b4487)
![Screenshot from 2024-10-21 23-35-47](https://github.com/user-attachments/assets/e2f157ed-0050-4309-abd4-8d75d155cfa0)
Realization of the Logic:
![Screenshot from 2024-10-21 23-35-59](https://github.com/user-attachments/assets/d2d8c776-91a5-4dac-b781-15e063c12e1c)

Netlist :
![Screenshot from 2024-10-21 23-37-25](https://github.com/user-attachments/assets/944b05a8-a69d-4108-8c97-629e5d667415)

### Day 3
### Combinational and Sequential Optimizations 
.
### Combinational Logic Optimization
**Why do we need Combinational Logic Optimizations?**

* Primarily to squeeze the logic to get the most optimized design.
    * An optimized design results in comprehensive Area and Power saving.

#### Types of Combinational Optimizations

* Constant Propagation 
	* Direct Optimization technique
* Boolean Logic Optimization.
	* Karnaugh map
	* Quine Mckluskey

#### CONSTANT PROPAGATION

In Constant propagation techniques, inputs that are no way related or affecting the changes in the output are ignored/optimized to simplify the combination logic thereby saving area and power usage by those input pins.
```
Y =((AB)+ C)'
If A = 0
Y =((0)+ C)' = C'
```
#### BOOLEAN LOGIC OPTIMIZATION

Boolean logic optimization is nothing simplifying a complex boolean expression into a simplified expression by utilizing the laws of boolean logic algebra.
```
assign y = a?(b?c:(c?a:0)):(!c)
```
above is simplified as
```
y = a'c' + a(bc + b'ca) 
y = a'c' + abc + ab'c 
y = a'c' + ac(b+b') 
y = a'c' + ac
y = a xnor c
```

### Sequential Logic Optimization

#### Types of Sequential Optimizations

* Basic Technique
	* Sequential Constant Propagation
* Advanced Technique
	* State Optimization
	* Retiming
	* Sequential Logic cloning(Floorplan aware synthesis)
	
#### COMBINATIONAL LOGIC OPTIMIZATION  

**2 input AND Gate**

```
module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog opt_check.v
synth -top opt_check
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
opt_clean -purge
show
```
![Screenshot from 2024-10-22 00-29-47](https://github.com/user-attachments/assets/0c187285-b6e4-4997-804d-ae2a03f46c2a)
![Screenshot from 2024-10-22 00-29-58](https://github.com/user-attachments/assets/236b9088-45ac-43d5-bc5a-58604b970cf2)
![Screenshot from 2024-10-22 00-30-11](https://github.com/user-attachments/assets/608a49f3-628b-4ee8-a516-a1a55912297c)
![Screenshot from 2024-10-22 00-30-58](https://github.com/user-attachments/assets/e01b7067-8011-4e9c-bda5-8e3e6f3c77b2)

**2 input OR Gate**
```
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule
```
```
 yosys
 read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog opt_check2.v
 synth -top opt_check2
 abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 opt_clean -purge
 show
```
![Screenshot from 2024-10-22 00-34-02](https://github.com/user-attachments/assets/1781c3f8-a60f-4cea-98bc-e295c1897ce5)
![Screenshot from 2024-10-22 00-34-15](https://github.com/user-attachments/assets/8b0b08fd-3f88-40ae-a892-d3277f616499)
![Screenshot from 2024-10-22 00-34-36](https://github.com/user-attachments/assets/dd133fdb-4037-4e0f-a191-46b5743c72c4)

 **3 input AND Gate**
 

```
 module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule

```

```
 yosys
 read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog opt_check3.v
 synth -top opt_check3
 abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 opt_clean -purge
 show
```

![Screenshot from 2024-10-22 00-37-07](https://github.com/user-attachments/assets/0b0dee2f-e083-4e95-b3ea-d169ea9c5892)
![Screenshot from 2024-10-22 00-37-18](https://github.com/user-attachments/assets/49e740b2-fb92-43ea-887d-d4b79c6a1e79)
![Screenshot from 2024-10-22 00-37-32](https://github.com/user-attachments/assets/1867c076-08bf-4e47-baef-c0a9a24edbae)
![Screenshot from 2024-10-22 00-37-43](https://github.com/user-attachments/assets/d60bded8-efef-480b-8c04-9a2a098ec7da)

**2 input XNOR Gate (3 input Boolean Logic)**

```
module opt_check4 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule
```

```
 yosys
 read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 read_verilog opt_check4.v
 synth -top opt_check4
 abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
 opt_clean -purge
 show
```
![Screenshot from 2024-10-22 00-41-04](https://github.com/user-attachments/assets/fc798c90-057f-4179-b998-8d2789886ba3)
![Screenshot from 2024-10-22 00-42-10](https://github.com/user-attachments/assets/58c1d949-5454-41cd-a953-5c8d7eb853a9)
![Screenshot from 2024-10-22 00-42-22](https://github.com/user-attachments/assets/87e91579-92bb-4070-a97a-aaadf96fbb54)


**Ex1**

```
module sub_module1(input a , input b , output y);
 assign y = a & b;
endmodule

module sub_module2(input a , input b , output y);
 assign y = a^b;
endmodule

module multiple_module_opt(input a , input b , input c , input d , output y);
wire n1,n2,n3;

sub_module1 U1 (.a(a) , .b(1'b1) , .y(n1));
sub_module2 U2 (.a(n1), .b(1'b0) , .y(n2));
sub_module2 U3 (.a(b), .b(d) , .y(n3));

assign y = c | (b & n1); 

endmodule
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_module_opt.v
synth -top multiple_module_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
flatten
show
write_verilog -noattr multiple_module_opt_net.v


gedit multiple_module_opt_net.v
```


On optimisation the above design becomes a AND OR gate

![Screenshot from 2024-10-22 00-46-54](https://github.com/user-attachments/assets/4a8e6c1c-f65a-4e7f-83a8-7470ea43b943)

![Screenshot from 2024-10-22 00-47-11](https://github.com/user-attachments/assets/835bb467-a71f-44fd-a283-9bf1899a41ef)

![Screenshot from 2024-10-22 00-47-30](https://github.com/user-attachments/assets/6ad2b6dc-a828-47c5-b83e-273654d7070b)

Realization of the Logic:

![Screenshot from 2024-10-22 01-28-28](https://github.com/user-attachments/assets/456ab910-4547-49de-a4c4-ac239455e632)


Netlist:

![Screenshot from 2024-10-22 00-48-20](https://github.com/user-attachments/assets/e5a97216-7b14-464d-ac18-b6e0933eb488)


**Ex2**

```
module sub_module(input a , input b , output y);
	assign y = a & b;
endmodule

module multiple_module_opt2(input a , input b , input c , input d , output y);
		wire n1,n2,n3;
	sub_module U1 (.a(a) , .b(1'b0) , .y(n1));
	sub_module U2 (.a(b), .b(c) , .y(n2));
	sub_module U3 (.a(n2), .b(d) , .y(n3));
	sub_module U4 (.a(n3), .b(n1) , .y(y));
endmodule
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog multiple_module_opt2.v
synth -top multiple_module_opt2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
flatten
show
write_verilog -noattr multiple_module_opt2_net.v
```

On optimisation the above design becomes Y=0

![Screenshot from 2024-10-22 00-52-40](https://github.com/user-attachments/assets/b0adbfe9-8780-4d28-a8ce-6fc0c474a406)

![Screenshot from 2024-10-22 00-52-58](https://github.com/user-attachments/assets/fc663317-a42a-47bc-83e8-3ecbaa93536e)
Realization of the Logic:
![Screenshot from 2024-10-22 01-26-27](https://github.com/user-attachments/assets/8863870b-fea0-4fd8-95cc-afbb22b63638)

Netlist:
![Screenshot from 2024-10-22 00-53-51](https://github.com/user-attachments/assets/690d1adb-5ec6-4aed-a434-0858c066be4c)

**Sequential Logic Optimizations**

**Ex 1**

```
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end
endmodule
```

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const1.v
synth -top dff_const1
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr dff_const1_net.v
```
```
iverilog dff_const1.v tb_dff_const1.v
./a.out
gtkwave tb_dff_const1.vcd
```


![Screenshot from 2024-10-22 00-58-06](https://github.com/user-attachments/assets/57970ccb-4153-4f57-a2ce-b138ebe60dea)

![Screenshot from 2024-10-22 00-58-23](https://github.com/user-attachments/assets/dbdf45bb-6805-4ada-9c83-c1e72b8b2bf5)

Realization of the Logic:

![Screenshot from 2024-10-22 00-58-35](https://github.com/user-attachments/assets/7c238db6-1a49-4443-adda-f838b69978e6)
Netlist:

![Screenshot from 2024-10-22 00-58-59](https://github.com/user-attachments/assets/bfea05c7-7e03-41af-89a6-78e048941f60)

Waveform:

![Screenshot from 2024-10-22 01-03-09](https://github.com/user-attachments/assets/e0fa19fb-0cd5-4198-b2c8-9cdcb5d827b9)

**Ex 2**

```
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end
endmodule
```

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const2.v
synth -top dff_const2
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr dff_const2_net.v

```
```
iverilog dff_const2.v tb_dff_const2.v
./a.out
gtkwave tb_dff_const2.vcd
```


![Screenshot from 2024-10-22 01-05-59](https://github.com/user-attachments/assets/cbb79e7a-8a41-4ec8-90be-259fc1f94097)

![Screenshot from 2024-10-22 01-06-09](https://github.com/user-attachments/assets/a2da2202-f858-4cd4-bdec-21f2939407f3)
Realization of the Logic:

![Screenshot from 2024-10-22 01-06-44](https://github.com/user-attachments/assets/5eedc405-5dd7-4c98-994d-728a31595efe)
Netlist:

![Screenshot from 2024-10-22 01-07-14](https://github.com/user-attachments/assets/d13e1f2b-513e-4ac2-8fa3-c4c12f0bfb5b)

![Screenshot from 2024-10-22 01-10-28](https://github.com/user-attachments/assets/a32be994-cce8-4a77-a595-7a0e346b2abd)

Waveform:
![Screenshot from 2024-10-22 01-10-20](https://github.com/user-attachments/assets/89e81e87-5092-4e2a-b711-6ac3cc9fccff)


**Ex3**

```
module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end
endmodule
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const3.v
synth -top dff_const3
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr dff_const3_net.v
```
```
iverilog dff_const3.v tb_dff_const3.v
./a.out
gtkwave tb_dff_const3.vcd
```

![Screenshot from 2024-10-22 01-10-28](https://github.com/user-attachments/assets/4851c075-0771-43de-97a1-d35abe736318)

![Screenshot from 2024-10-22 01-12-55](https://github.com/user-attachments/assets/cdd9b747-8361-46e3-9d1e-ee510acc9d96)

![Screenshot from 2024-10-22 01-13-13](https://github.com/user-attachments/assets/630fa259-f2c8-4421-acaf-9ec1aed31a53)


Realization of the Logic:
![Screenshot from 2024-10-22 01-13-34](https://github.com/user-attachments/assets/cdeab5d6-042a-4429-b717-b8373696ca9a)
Netlist:

![Screenshot from 2024-10-22 01-14-07](https://github.com/user-attachments/assets/955b82cc-1295-479b-ad56-aa866e8e0eaf)


![Screenshot from 2024-10-22 01-16-35](https://github.com/user-attachments/assets/414c5a2f-90b8-4ab6-aa22-75c83da8e992)
Waveform:

![Screenshot from 2024-10-22 01-16-13](https://github.com/user-attachments/assets/ed4fef46-c5c7-4350-804f-1c35085529dc)


**Ex 4**

```
module dff_const4(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b1;
	end
else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end
endmodule
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const4.v
synth -top dff_const4
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr dff_const4_net.v
```
```
iverilog dff_const4.v tb_dff_const4.v
./a.out
gtkwave tb_dff_const4.vcd
```
![Screenshot from 2024-10-22 01-33-55](https://github.com/user-attachments/assets/b8ecf2c8-be4c-4833-93a2-4d2a45eec581)
Realization of the Logic:
![Screenshot from 2024-10-22 01-34-27](https://github.com/user-attachments/assets/02e81954-513c-4038-aec8-60d6b56d55ae)
Netlist:
![Screenshot from 2024-10-22 01-35-06](https://github.com/user-attachments/assets/b84c3377-499e-4cfe-904c-b50844dde0e8)

![Screenshot from 2024-10-22 01-36-47](https://github.com/user-attachments/assets/1dda8622-127b-4c60-a73a-a71c2fa93677)
Waveform:
![Screenshot from 2024-10-22 01-36-31](https://github.com/user-attachments/assets/42f730f8-9db2-4780-b195-53fd50e889e9)

**Ex5**

```
module dff_const5(input clk, input reset, output reg q);
reg q1;
always @(posedge clk, posedge reset)
	begin
		if(reset)
		begin
			q <= 1'b0;
			q1 <= 1'b0;
		end
	else
		begin
			q1 <= 1'b1;
			q <= q1;
		end
	end
endmodule
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_const5.v
synth -top dff_const5
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr dff_const5_net.v
```
```
iverilog dff_const5.v tb_dff_const5.v
./a.out
gtkwave tb_dff_const5.vcd
```
![Screenshot from 2024-10-22 01-36-47](https://github.com/user-attachments/assets/66507a1f-d1b7-4fba-a7f6-e47d91825015)

![Screenshot from 2024-10-22 01-40-13](https://github.com/user-attachments/assets/07b2f451-f905-41c9-a261-19e2e70773d9)

![Screenshot from 2024-10-22 01-40-31](https://github.com/user-attachments/assets/e56ddc82-c319-46a7-b524-ba9f16b47ef5)
Realization of the Logic:
![Screenshot from 2024-10-22 01-40-49](https://github.com/user-attachments/assets/4a741022-b4e2-4f48-a35b-2ea6e7866d77)
Netlist:

![Screenshot from 2024-10-22 01-41-16](https://github.com/user-attachments/assets/6861246d-bfb5-4914-9379-4d4e3e987597)

Waveform:
![Screenshot from 2024-10-22 01-42-42](https://github.com/user-attachments/assets/6e1a2a54-68f8-4575-9390-b73aa4cb9ead)

![Screenshot from 2024-10-22 01-44-00](https://github.com/user-attachments/assets/a75ca931-6a73-42df-afa1-e3eaeb820477)

**Sequential Logic Optimizations for unused outputs**

```
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = count[0];
always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end
endmodule
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt.v
synth -top counter_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr counter_opt_net.v
```
```
iverilog counter_opt.v tb_counter_opt.v
./a.out
gtkwave tb_counter_opt.vcd
```

![Screenshot from 2024-10-22 01-45-45](https://github.com/user-attachments/assets/84c15a47-3bc9-4edd-9ea1-f46923b2d73e)
![Screenshot from 2024-10-22 01-46-03](https://github.com/user-attachments/assets/e965746e-39ad-410d-ab85-8afbddbb9bce)
Realization of the Logic:
![Screenshot from 2024-10-22 01-46-17](https://github.com/user-attachments/assets/e2b5f79f-e638-4f1a-9277-01c82908e4a4)
Netlist:
![Screenshot from 2024-10-22 01-46-51](https://github.com/user-attachments/assets/1790aab2-6363-433d-baa0-ad472cac0d89)

![Screenshot from 2024-10-22 01-48-54](https://github.com/user-attachments/assets/469252a7-c9bb-4a1f-8fb6-a85fd071db5c)
Waveform:
![Screenshot from 2024-10-22 01-48-48](https://github.com/user-attachments/assets/26cd2645-4faa-4c89-83df-37bc8b82bde2)

**Modified counter logic:**

```
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = {count[2:0]==3'b100};
always @(posedge clk ,posedge reset)
begin
if(reset)
	count <= 3'b000;
else
	count <= count + 1;
end
endmodule
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog counter_opt2.v
synth -top counter_opt
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr counter_opt_net.v
```
```
iverilog counter_opt.v tb_counter_opt.v
./a.out
gtkwave tb_counter_opt.vcd
```

![Screenshot from 2024-10-22 01-55-35](https://github.com/user-attachments/assets/ae3fe546-48b1-425a-b82a-85837c01e54e)
![Screenshot from 2024-10-22 01-55-57](https://github.com/user-attachments/assets/de96448c-ab2d-4e80-b35f-da75957f7a50)
Realization of the Logic:
![Screenshot from 2024-10-22 01-56-08](https://github.com/user-attachments/assets/f1a27261-77b3-41aa-9997-26161c60fa2c)

Netlist:
![Screenshot from 2024-10-22 01-56-31](https://github.com/user-attachments/assets/6a43bb47-4e08-40aa-bf9a-559b14c7f074)

![Screenshot from 2024-10-22 01-57-35](https://github.com/user-attachments/assets/7b05260d-4112-41b7-8335-e4e3cfd076fa)

Waveform:

![Screenshot from 2024-10-22 01-57-25](https://github.com/user-attachments/assets/ab377d26-0442-409a-a379-405cc5e3f037)








### Day 4

### GLS, blocking vs non-blocking and Synthesis-Simulation mismatch

Gate Level Simulation (GLS) is a crucial step in the verification process of digital circuits. It involves simulating the synthesized netlist, which is a lower-level representation of the design, using a testbench to verify its logical correctness and timing behavior. By comparing the simulated outputs to the expected outputs, GLS ensures that the synthesis process has not introduced any errors and that the design meets its performance requirements.


<img width="855" alt="gls" src="https://github.com/user-attachments/assets/71f189c5-2b1b-48b1-b33d-bdb34132658f">

Sensitivity lists are crucial for accurate circuit behavior. If a sensitivity list is incomplete, it can lead to unexpected latches. Blocking and non-blocking assignments within always blocks have different execution behaviors. Incorrect use of blocking assignments can unintentionally create latches, causing synthesis and simulation mismatches. To avoid these issues, it's essential to carefully analyze circuit behavior and ensure that the sensitivity list and assignments align with the desired functionality.

**GLS Simulation**
**Ex 1**
Code:
![Screenshot from 2024-10-21 23-44-50](https://github.com/user-attachments/assets/a20c992d-676b-4251-a379-9ba874fc86c7)

```
iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog ternary_operator_mux.v
synth -top ternary_operator_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
write_verilog -noattr ternary_operator_mux_net.v
```

![Screenshot from 2024-10-21 23-45-50](https://github.com/user-attachments/assets/488e793d-6687-4845-b1a8-3cdb10c72835)
![Screenshot from 2024-10-21 23-46-34](https://github.com/user-attachments/assets/d6732790-e249-4020-816e-4f461e260dc9)


![Screenshot from 2024-10-21 23-48-47](https://github.com/user-attachments/assets/e5fb80bf-47f9-46fd-b503-945b54ba0201)

![Screenshot from 2024-10-21 23-48-40](https://github.com/user-attachments/assets/e72c77fa-519d-4e12-baf6-b609f748968a)

![Screenshot from 2024-10-21 23-49-00](https://github.com/user-attachments/assets/b988c59a-b14f-43e0-bb53-4cba16db235e)

Realization of the Logic:
![Screenshot from 2024-10-21 23-49-11](https://github.com/user-attachments/assets/fc34debb-e4c6-4f87-9254-3625e0b5cf7e)
Netlist:
![Screenshot from 2024-10-21 23-49-46](https://github.com/user-attachments/assets/ad0ad49f-429c-4e78-8e84-00b89ca7813d)

GLS

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```
Waveform:
In this case there is no mismatch between the waveforms before and after synthesis

![Screenshot from 2024-10-21 23-54-03](https://github.com/user-attachments/assets/693c696e-e6b2-43bf-a11d-6ba6e684b3a2)


**Ex 2:**

```
module bad_mux (input i0 , input i1 , input sel , output reg y);
always @ (sel)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```
```
iverilog bad_mux.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog bad_mux.v
synth -top bad_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
write_verilog -noattr bad_mux_net.v
```

Waveform:


![Screenshot from 2024-10-21 23-58-24](https://github.com/user-attachments/assets/5e36ad19-3280-43b7-9f40-2d190141ea37)


![Screenshot from 2024-10-22 00-00-34](https://github.com/user-attachments/assets/f9bb0ee1-9d84-451c-811d-3f39ec42d37f)



![Screenshot from 2024-10-22 00-00-48](https://github.com/user-attachments/assets/56fcd6a7-bfe7-465a-a9ef-f6e74ddaf46f)

Realization of logic:

![Screenshot from 2024-10-22 00-01-00](https://github.com/user-attachments/assets/efc735ac-e45c-465b-94ab-8d0c188b29a9)

Netlist:
![Screenshot from 2024-10-22 00-03-57](https://github.com/user-attachments/assets/c90db12b-3bd6-44f5-8e13-3197bf91ad96)

GLS:

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```

Waveform:
In this case there is a synthesis and simulation mismatch. While performing synthesis yosys has corrected the sensitivity list error.

![Screenshot from 2024-10-22 00-06-06](https://github.com/user-attachments/assets/b0a8e1f7-e4e0-4354-b065-b67aaac29870)

**Labs:Synthesis-Simulation mismatch for blocking statements**

```
module blocking_caveat (input a , input b , input  c, output reg d); 
reg x;
always @ (*)
begin
d = x & c;
x = a | b;
end
endmodule
```
```
iverilog blocking_caveat.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```
```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog blocking_caveat.v
synth -top blocking_caveat
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
write_verilog -noattr blocking_caveat_net.v
```

![Screenshot from 2024-10-22 00-15-25](https://github.com/user-attachments/assets/d0cd66af-b4f4-4b31-bcb8-7b22bd661127)
Waveform:

![Screenshot from 2024-10-22 00-14-50](https://github.com/user-attachments/assets/8b9d7dea-46b3-404f-91ce-67215e24b7cc)


![Screenshot from 2024-10-22 00-16-22](https://github.com/user-attachments/assets/2fbbe333-f7c1-42ea-a544-5e9708c57c04)
![Screenshot from 2024-10-22 00-16-32](https://github.com/user-attachments/assets/dfff4ba3-7433-49b8-b35c-c8612eec746b)
Realization of Logic:
![Screenshot from 2024-10-22 00-16-46](https://github.com/user-attachments/assets/25b7f38b-0664-4501-a4ee-54648aa9a8f7)
Netlist:
![Screenshot from 2024-10-22 00-17-22](https://github.com/user-attachments/assets/1958e816-f25e-4343-bec4-511daba2038f)

GLS:

```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```

![Screenshot from 2024-10-22 00-22-09](https://github.com/user-attachments/assets/d27f66a8-7bd7-4991-9ab3-0c03a1b4eafe)


Waveform:
In this case there is a synthesis and simulation mismatch. While performing synthesis yosys has corrected the latch error.

![Screenshot from 2024-10-22 00-20-35](https://github.com/user-attachments/assets/82614321-d1a0-4af1-bff3-cccacc111946)



## Assignment 11

### To Synthesize RISC-V and compare output with functional simulations.



```
 cp -r src sky130RTLDesignAndSynthesisWorkshop/
 cd sky130RTLDesignAndSynthesisWorkshop/
 ls
 cd src
 cd module/
```
Here take src folder from VSDBabySoc folder and Copy the src folder from your VSDBabySoC folder to your ASIC folder.

### Synthesis:

```
yosys
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -lib ../lib/avsddac.lib
read_liberty -lib ../lib/avsdpll.lib  
read_verilog ../module/vsdbabysoc.v
read_verilog ../module/rvmyth.v
read_verilog ../module/clk_gate.v 
synth -top vsdbabysoc
dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
show
write_verilog -noattr vsdbabysoc.synth.v
exit
```
![Screenshot from 2024-10-24 01-03-34](https://github.com/user-attachments/assets/e82bd0d2-e234-4f06-a228-3d064e543db1)
synthesized module
![Screenshot from 2024-10-24 01-10-17](https://github.com/user-attachments/assets/e44b9581-8230-461b-ae04-ca4e7f3355eb)

Netlist code:
![Screenshot from 2024-10-24 01-14-19](https://github.com/user-attachments/assets/d9b452f2-a660-411a-b706-cf346c396f45)



```
yosys 
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog clk_gate.v
read_verilog rvmyth.v
synth -top rvmyth
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog -noattr rvmyth.v
!gedit rvmyth.v
exit
```
```
iverilog ../../my_lib/verilog_model/primitives.v ../../my_lib/verilog_model/sky130_fd_sc_hd.v rvmyth.v testbench.v vsdbabysoc.v avsddac.v avsdpll.v 
./a.out
gtkwave dump.vcd
```
![Screenshot from 2024-10-23 23-43-16](https://github.com/user-attachments/assets/be55fed9-596e-4e9a-b3e7-852daa448ec9)
Synthesis:
![Screenshot from 2024-10-23 23-50-16](https://github.com/user-attachments/assets/07b7e7ee-a647-45f8-a1ac-e3f4f13b1ca3)
![Screenshot from 2024-10-23 23-50-28](https://github.com/user-attachments/assets/b0552a1e-2d76-447a-adad-2d0ff9cc9d97)
![Screenshot from 2024-10-23 23-50-46](https://github.com/user-attachments/assets/31d7a766-2aaa-4935-bfad-123792824297)
NetList:
![Screenshot from 2024-10-23 23-51-43](https://github.com/user-attachments/assets/79fd6f57-93b1-45cc-840d-c871e4379d91)

Waveform:
![Screenshot from 2024-10-24 00-00-13](https://github.com/user-attachments/assets/8946d5d0-8c2f-45fe-af9a-a809f0680a3d)
![Screenshot from 2024-10-24 00-00-33](https://github.com/user-attachments/assets/d916729c-00b5-4456-a055-1da6844a1cec)
![Screenshot from 2024-10-24 00-00-42](https://github.com/user-attachments/assets/97900cbf-224f-4992-88ff-6e556d68a396)
![Screenshot from 2024-10-24 02-02-31](https://github.com/user-attachments/assets/a368c6cb-2bca-4008-93a0-48f3f7b9d6ca)

With cells:
![Screenshot from 2024-10-24 01-43-57](https://github.com/user-attachments/assets/6d627c97-e6f5-4294-b019-5659055cdcd5)




### Functional Simulations

```
cd
cd VSDBabySoC
iverilog -o ./pre_synth_sim.out -DPRE_SYNTH_SIM src/module/testbench.v -I src/include -I src/module/
./pre_synth_sim.out
gtkwave pre_synth_sim.vcd
```
![Screenshot from 2024-10-24 00-01-47](https://github.com/user-attachments/assets/93beb236-d91a-43f5-afb8-52b5911f5899)

Waveform:
![Screenshot from 2024-10-24 01-28-00](https://github.com/user-attachments/assets/6ba0d3a7-cb5f-46b5-8ce4-c4a9b3a4e6bb)
![Screenshot from 2024-10-24 01-28-13](https://github.com/user-attachments/assets/1ae12913-19b7-411f-b14e-dd4299a7e390)
![Screenshot from 2024-10-24 01-30-00](https://github.com/user-attachments/assets/8e9ca955-5da6-45b4-b89c-71c292e84167)
![Screenshot from 2024-10-24 01-30-58](https://github.com/user-attachments/assets/6547d6ff-9683-4613-8b9e-aa598aa0043e)



As we can see comparing The Functionality vs Synthesized output waveform matches hence verifying our results.

![Screenshot from 2024-10-24 01-58-12](https://github.com/user-attachments/assets/08d1dd05-d313-406f-9eea-022080d50cbd)

![Screenshot from 2024-10-24 01-43-25](https://github.com/user-attachments/assets/61ec933b-4551-49ab-a201-d7bc8ffbca56)
![Screenshot from 2024-10-24 01-43-39](https://github.com/user-attachments/assets/2173fec4-aee7-418e-b2e9-21febe94580c)


## Assignment 12
### Post Synthesis Static Timing Analysis using OpenSTA

### STA
Static Timing Analysis (STA) is a method used in digital circuit design to verify the timing performance of a circuit without requiring dynamic simulation. It checks whether the circuit meets its timing constraints by analyzing the timing paths in the design. Here are some key aspects of STA:
Timing Paths: STA evaluates all possible paths through a circuit from input to output, taking into account the propagation delays of gates and interconnects.
Setup and Hold Times: It checks for setup and hold time violations. The setup time is the minimum time before the clock edge that the input data must be stable, while the hold time is the minimum time after the clock edge that the data must remain stable.
Clock Constraints: STA incorporates clock definitions, including the clock frequency, period, and any variations (like skew or jitter).
Worst-case Scenario: STA assumes worst-case conditions for delay values (like maximum load, temperature, and voltage) to ensure that the circuit will perform correctly under all expected operating conditions.
Tools: There are various tools for performing STA, such as Synopsys PrimeTime, Cadence Tempus, and others, which automate the process and provide detailed reports on timing violations. Overall, STA is crucial for ensuring that digital circuits operate reliably at the intended speeds and for identifying potential timing issues early in the design process.

### Reason for STA:
Static Timing Analysis (STA) is performed for several critical reasons in digital circuit design:

Timing Verification: STA ensures that the design meets its specified timing constraints. It verifies that data signals can propagate through the circuit within the required time limits, ensuring that outputs are stable and valid when needed.
Identify Timing Violations: It helps identify setup and hold time violations, which can lead to incorrect operation of flip-flops and other sequential elements. Detecting these violations is crucial to ensure the reliability of the circuit.
Performance Optimization: By analyzing the timing paths, designers can identify critical paths that limit the maximum operating frequency. This information can be used to optimize the design by resizing gates, adjusting the layout, or modifying the clock strategy.
Early Detection of Issues: STA allows for early detection of timing issues during the design process, reducing the risk of costly iterations and revisions in later stages, such as post-layout or during fabrication.
Power Consumption Analysis: Timing analysis can also help in understanding the impact of clock frequency on power consumption. By ensuring that the design runs at optimal speeds, designers can balance performance and power efficiency.

### vsdbabysoc_synthesis.sdc:
```
set PERIOD 11.20
set_units -time ns
create_clock [get_pins {pll/CLK}] -name clk -period $PERIOD
set_clock_uncertainty -setup  [expr $PERIOD * 0.05] [get_clocks clk]
set_clock_transition [expr $PERIOD * 0.05] [get_clocks clk]
set_clock_uncertainty -hold [expr $PERIOD * 0.08] [get_clocks clk]
set_input_transition [expr $PERIOD * 0.08] [get_ports ENb_CP]
set_input_transition [expr $PERIOD * 0.08] [get_ports ENb_VCO]
set_input_transition [expr $PERIOD * 0.08] [get_ports REF]
set_input_transition [expr $PERIOD * 0.08] [get_ports VCO_IN]
set_input_transition [expr $PERIOD * 0.08] [get_ports VREFH]
```
### Running the OpenSTA:
```
cd VSDBabySoc/src
sta
read_liberty -min ./lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -min ./lib/avsdpll.lib
read_liberty -min ./lib/avsddac.lib
read_liberty -max ./lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_liberty -max ./lib/avsdpll.lib
read_liberty -max ./lib/avsddac.lib
read_verilog ../output/synth/vsdbabysoc.synth.v
link_design vsdbabysoc
read_sdc ./sdc/vsdbabysoc_synthesis.sdc
report_checks -path_delay min_max -format full_clock_expanded -digits 4
```


![Screenshot from 2024-10-28 21-54-06](https://github.com/user-attachments/assets/ef64b544-5aa8-4a27-a183-60dd996c7fb6)

HOLD TIME:
![Screenshot from 2024-10-29 00-11-55](https://github.com/user-attachments/assets/836a5209-2785-4e6b-9624-455796f20cd0)


![Screenshot from 2024-10-29 00-12-42](https://github.com/user-attachments/assets/be82d44a-5ab6-4f22-a18f-ece111c88c3f)

SETUP TIME:
![Screenshot from 2024-10-29 00-11-47](https://github.com/user-attachments/assets/247c4adc-96b5-498f-895e-77c4fbf982e4)


## Assignment 13
Post Synthesis Static Timing Analysis using OpenSTA for all the sky130 lib files.

```
set PERIOD 11.20
set_units -time ns
create_clock [get_pins {pll/CLK}] -name clk -period $PERIOD
set_clock_uncertainty -setup  [expr $PERIOD * 0.05] [get_clocks clk]
set_clock_transition [expr $PERIOD * 0.05] [get_clocks clk]
set_clock_uncertainty -hold [expr $PERIOD * 0.08] [get_clocks clk]
set_input_transition [expr $PERIOD * 0.08] [get_ports ENb_CP]
set_input_transition [expr $PERIOD * 0.08] [get_ports ENb_VCO]
set_input_transition [expr $PERIOD * 0.08] [get_ports REF]
set_input_transition [expr $PERIOD * 0.08] [get_ports VCO_IN]
set_input_transition [expr $PERIOD * 0.08] [get_ports VREFH]
```


Store all the lib files in a folder  timing_libs(in src)
Create a sta_pvt.tcl file with below content:

```
set list_of_lib_files(1) "sky130_fd_sc_hd__ff_100C_1v65.lib"
set list_of_lib_files(2) "sky130_fd_sc_hd__ff_100C_1v95.lib"
set list_of_lib_files(3) "sky130_fd_sc_hd__ff_n40C_1v56.lib"
set list_of_lib_files(4) "sky130_fd_sc_hd__ff_n40C_1v65.lib"
set list_of_lib_files(5) "sky130_fd_sc_hd__ff_n40C_1v76.lib"
set list_of_lib_files(6) "sky130_fd_sc_hd__ff_n40C_1v95.lib"
set list_of_lib_files(7) "sky130_fd_sc_hd__ff_n40C_1v95_ccsnoise.lib.part1"
set list_of_lib_files(8) "sky130_fd_sc_hd__ff_n40C_1v95_ccsnoise.lib.part2"
set list_of_lib_files(9) "sky130_fd_sc_hd__ff_n40C_1v95_ccsnoise.lib.part3"
set list_of_lib_files(10) "sky130_fd_sc_hd__ss_100C_1v40.lib"
set list_of_lib_files(11) "sky130_fd_sc_hd__ss_100C_1v60.lib"
set list_of_lib_files(12) "sky130_fd_sc_hd__ss_n40C_1v28.lib"
set list_of_lib_files(13) "sky130_fd_sc_hd__ss_n40C_1v35.lib"
set list_of_lib_files(14) "sky130_fd_sc_hd__ss_n40C_1v40.lib"
set list_of_lib_files(15) "sky130_fd_sc_hd__ss_n40C_1v44.lib"
set list_of_lib_files(16) "sky130_fd_sc_hd__ss_n40C_1v60.lib"
set list_of_lib_files(17) "sky130_fd_sc_hd__ss_n40C_1v60_ccsnoise.lib.part1"
set list_of_lib_files(18) "sky130_fd_sc_hd__ss_n40C_1v60_ccsnoise.lib.part2"
set list_of_lib_files(19) "sky130_fd_sc_hd__ss_n40C_1v60_ccsnoise.lib.part3"
set list_of_lib_files(20) "sky130_fd_sc_hd__ss_n40C_1v76.lib"
set list_of_lib_files(21) "sky130_fd_sc_hd__tt_025C_1v80.lib"
set list_of_lib_files(22) "sky130_fd_sc_hd__tt_100C_1v80.lib"

for {set i 1} {$i <= [array size list_of_lib_files]} {incr i} {
read_liberty ./timing_libs/$list_of_lib_files($i)
read_verilog ../output/synth/vsdbabysoc.synth.v
link_design vsdbabysoc
read_sdc ./sdc/vsdbabysoc_synthesis.sdc
check_setup -verbose
report_checks -path_delay min_max -fields {nets cap slew input_pins fanout} -digits {4} > ./sta_output/min_max_$list_of_lib_files($i).txt

}
```
Create a folder named sta_output in VSDBabySoC/src. .txt files will be generated.
```
cd VSDBabySoC/src
sta
source sta_pvt.tcl
```

![Screenshot from 2024-11-05 03-38-04](https://github.com/user-attachments/assets/e88856c5-9297-40b6-9f57-9b67399b912e)
![Screenshot from 2024-11-05 01-50-12](https://github.com/user-attachments/assets/ae13b57b-d94a-46a7-91cf-f76b64f146a8)
![Screenshot from 2024-11-05 03-26-26](https://github.com/user-attachments/assets/ba7f5f77-f44e-4d9a-89b3-a3dc84709ce8)
![Screenshot from 2024-11-05 03-28-11](https://github.com/user-attachments/assets/265f738d-092c-4b74-998b-be57d6d7f8f4)

| File Name                                     | Worst HoldSlack (WNS) | Worst Negative Slack (WNS) |
|-----------------------------------------------|------------------------|-----------------------------|
| min_max_sky130_fd_sc_hd__ff_100C_1v65.lib.txt | -0.6057               | -3.2129                     |
| min_max_sky130_fd_sc_hd__ff_n40C_1v95.lib.txt | -0.6648               | 0.0555                      |
| min_max_sky130_fd_sc_hd__ff_n40C_1v56.lib.txt | -0.544                | -2.8771                     |
| min_max_sky130_fd_sc_hd__ff_n40C_1v65.lib.txt | -0.5847               | -1.7646                     |
| min_max_sky130_fd_sc_hd__ff_n40C_1v76.lib.txt | -0.621                | -0.8431                     |
| min_max_sky130_fd_sc_hd__ff_n40C_1v95.lib.txt | -0.6648               | 0.0555                      |
| min_max_sky130_fd_sc_hd__ff_n40C_1v95_ccsnoise.lib.part1.txt | -0.6648 | 0.0555          |
| min_max_sky130_fd_sc_hd__ff_n40C_1v95_ccsnoise.lib.part2.txt | -0.6648 | 0.0555          |
| min_max_sky130_fd_sc_hd__ff_n40C_1v95_ccsnoise.lib.part3.txt | -0.6648 | 0.0555          |
| min_max_sky130_fd_sc_hd__ss_100C_1v40.lib.txt | 0.1376                | -25.9157                    |
| min_max_sky130_fd_sc_hd__ss_100C_1v60.lib.txt | -0.1424               | -15.7276                    |
| min_max_sky130_fd_sc_hd__ss_n40C_1v28.lib.txt | 1.0372                | -96.7958                    |
| min_max_sky130_fd_sc_hd__ss_n40C_1v35.lib.txt | 0.5733                | -60.9135                    |
| min_max_sky130_fd_sc_hd__ss_n40C_1v44.lib.txt | 0.2112                | -38.9537                    |
| min_max_sky130_fd_sc_hd__ss_n40C_1v60.lib.txt | -0.1213               | -19.6409                    |
| min_max_sky130_fd_sc_hd__ss_n40C_1v60_ccsnoise.lib.part1.txt | -0.1213 | -19.6409        |
| min_max_sky130_fd_sc_hd__ss_n40C_1v60_ccsnoise.lib.part2.txt | -0.1213 | -19.6409        |
| min_max_sky130_fd_sc_hd__ss_n40C_1v60_ccsnoise.lib.part3.txt | -0.1213 | -19.6409        |
| min_max_sky130_fd_sc_hd__tt_025C_1v80.lib.txt | -0.5417               | -4.2481                     |
| min_max_sky130_fd_sc_hd__tt_100C_1v80.lib.txt | -0.5439               | -5.1643                     |

Graphs plotted in LibreOffice Calc using all values taken from txts.
### Worst Negative Slack(Graph)
![Screenshot from 2024-11-05 03-32-38](https://github.com/user-attachments/assets/4767f300-3531-4aee-a2c9-31da5acbf64f)
### Worst Hold Slack(Graph)
![Screenshot from 2024-11-05 03-30-09](https://github.com/user-attachments/assets/8b31e76e-0d82-4c35-8969-9415c75d6738)


## Assignment 14

#### Day-1: Inception of open-source EDA, OpenLane and Sky130 PDK

**QFN-48 Package:** A Quad Flat No-leads (QFN) 48 package is a leadless IC package with 48 connection pads around the perimeter. It offers good thermal and electrical performance in a compact form, making it ideal for high-density applications.

![image](https://github.com/user-attachments/assets/2237a9ef-dc38-444f-97a5-ceb4e983c8f0)


**Chip:** An integrated circuit (IC) that contains various functional blocks like memory, processing units, and I/O in a silicon substrate, typically used for specific applications in electronics.

![image](https://github.com/user-attachments/assets/7503bcea-4654-4bc9-b77a-de9ced7929be)


**Pads:** Small metallic areas on a chip or package used to connect internal circuitry to external connections, enabling signals to be transferred to and from the IC.

**Core:** The central part of a chip containing the main processing unit and functional logic, often optimized for power and performance.

**Die:** The section of a silicon wafer containing an individual IC before it is packaged, housing all active circuits and elements for the chip's functions.

![image](https://github.com/user-attachments/assets/cfa2c482-59c5-4ad5-b74c-a027bfdf16b8)

**IPs (Intellectual Properties):** Pre-designed functional blocks or modules within a chip, such as USB controllers or memory interfaces, licensed for reuse across various designs to save time and cost.

![image](https://github.com/user-attachments/assets/1039a7d9-0286-42c7-8da7-17136c3da5aa)


**From Software Applications to Hardware Flow**

To run an application on hardware, several processes take place. First, the application enters a layer known as the system software, which prepares it for execution by translating the application program into binary format, understandable by hardware. Key components within system software include the Operating System (OS), Compiler, and Assembler.

The process starts with the OS, which breaks down application functions written in high-level languages such as C, C++, Java, or Visual Basic. These functions are passed to a suitable compiler, which translates them into low-level instructions. The syntax and format of these instructions are tailored to the specific hardware architecture in use.

Next, the assembler converts these hardware-specific instructions into binary format, known as machine language. This binary code is then fed to the hardware, enabling it to perform specific tasks as defined by the received instructions.

![image](https://github.com/user-attachments/assets/14788472-7c91-4860-82c6-2bccb49f91d2)

For example, consider a stopwatch app running on a RISC-V core. Here, the OS might generate a small function in C, which is then passed to a compiler. The compiler outputs RISC-V-specific instructions, tailored to the architecture. These instructions are subsequently processed by the assembler, which converts them into binary code. This binary code then flows into the chip layout, where the hardware executes the desired functionality.

![image](https://github.com/user-attachments/assets/cabbd8f7-f0c4-4a13-bf2e-d6d67392910e)

For the above stopwatch the below figure shows the input and output of the compiler and assembler.

![image](https://github.com/user-attachments/assets/63f2e771-eed8-4953-b501-dd9ff0d209f7)

The compiler generates architecture-specific instructions, while the assembler produces the corresponding binary patterns. To execute these instructions on hardware, an RTL (written in a Hardware Description Language) is used to interpret and implement the instructions. This RTL design is then synthesized into a netlist, represented as interconnected logic gates. Finally, the netlist undergoes physical design implementation to be fabricated onto the chip.

![image](https://github.com/user-attachments/assets/ae0a287d-8bb4-4535-b6b0-5b1baf09008d)

**Components of ASIC Design**

![image](https://github.com/user-attachments/assets/560b728b-8e75-4c9d-a3c8-5b640318c4aa)

- RTL IPs: Pre-designed, verified digital circuit blocks (like adders, flip-flops, memory) in HDL (e.g., Verilog, VHDL). They save design time by providing ready-to-use components for complex circuits.

- EDA Tools: Software that automates ASIC design tasks (e.g., synthesis, optimization, placement, timing analysis). Essential for improving productivity and ensuring performance and power requirements are met.

- PDK Data: A set of files and parameters from a semiconductor foundry, detailing its manufacturing process (e.g., transistor models, design rules). PDKs ensure ASIC designs are compatible with the foundry’s fabrication process.

**Simplified RTL to GDS flow**

![image](https://github.com/user-attachments/assets/1f2a5455-d83e-46fe-92e3-531ade2a9add)

- **RTL Design:** Describes the circuit's functional behavior using HDLs like Verilog or VHDL, defining its logic and data paths.

- **RTL Synthesis:** Converts RTL code to a gate-level netlist which is a collection of standard cells like AND gates, flip-flops, and multiplexers by mapping it to standard cells and optimizing for area, power, and timing. 
- **Floor and Power Planning:** Partitions chip area, places major components, and defines power grid and I/O placement to optimize area, power distribution, and signal flow. This step optimizes the physical layout, aiming to reduce power consumption and improve signal integrity by considering the placement of I/O pads and power distribution cells

- **Placement:** Assigns physical locations to cells, aiming to minimize wirelength, reduce signal delay, and meet design constraints. The placement tool carefully arranges the cells to balance the overall chip design for optimal performance and area utilization.

- **Clock Tree Synthesis (CTS):** Clock Tree Synthesis (CTS) is a critical step that focuses on creating an optimized clock distribution network. CTS ensures the clock is distributed evenly to all flip-flops and registers. It builds an optimized clock network to balance clock signal distribution and reduce clock skew.

- **Routing:** Connects components based on placement, optimizing wire paths to ensure signal integrity, minimize congestion, and meet design rules.

- **Sign-off:** Final verification stage, ensuring the design meets functionality, performance, power, and reliability targets. Timing analysis is performed to check setup and hold times, power analysis ensures the design doesn’t exceed power limits, and physical verification checks ensure that the layout meets manufacturing rules. This stage confirms the design is ready for fabrication.

- **GDSII File Generation:** Creates the GDSII file containing the complete layout details needed for chip fabrication. This file represents the final physical design and is used by manufacturers to create the photomasks required for chip production. The GDSII file serves as the blueprint for the actual fabrication of the chip.

**OpenLane ASIC Flow:**

![image](https://github.com/user-attachments/assets/cdd04b14-fbfe-44a3-8d4e-8fbfe443bd74)

1. RTL Synthesis, Technology Mapping, and Formal Verification: The tools used are Yosys (for RTL synthesis), ABC (for technology mapping and formal verification).
2. Static Timing Analysis: The tools used are OpenSTA (for static timing analysis).
3. Floor Planning: The tools used are init_fp (initial floorplanning), ioPlacer (I/O placement), pdn (power distribution network planning), tapcell (tap cell insertion).
4. Placement: The tools used are RePLace (global placement), Resizer (optional for resizing cells), OpenPhySyn (formerly used for placement), OpenDP (detailed placement).
5. Clock Tree Synthesis: The tools used are TritonCTS (for clock tree synthesis).
6. Fill Insertion: The tools used are OpenDP (for filler placement).
7. Routing: The tools used for global routing are FastRoute or CU-GR (formerly used) and for the detailed routing , we use TritonRoute (for detailed routing) or DR-CU (formerly used).
8. SPEF Extraction: The tools used are OpenRCX (or SPEF-Extractor, formerly used) for Standard Parasitic Exchange Format (SPEF) extraction.
9. GDSII Streaming Out: The tools used are Magic and KLayout (for viewing and editing GDSII files).
10. Design Rule Checking (DRC) Checks: The tools used are Magic and KLayout (for DRC checks).
11. Layout vs. Schematic (LVS) Check: The tools used are Netgen (for LVS checks).
12. Antenna Checks: The tools used are Magic (for antenna checks).

**OpenLANE Directory structure**

``` 
├── OOpenLane             -> directory where the tool can be invoked (run docker first)
│   ├── designs          -> All designs must be extracted from this folder
│   │   │   ├── picorv32a -> Design used as case study for this workshop
│   |   |   ├── ...
|   |   ├── ...
├── pdks                 -> contains pdk related files 
│   ├── skywater-pdk     -> all Skywater 130nm PDKs
│   ├── open-pdks        -> contains scripts that makes the commerical PDK (which is normally just compatible to commercial tools) to also be compatible with the open-source EDA tool
│   ├── sky130A          -> pdk variant made especially compatible for open-source tools
│   │   │  ├── libs.ref  -> files specific to node process (timing lib, cell lef, tech lef) for example is `sky130_fd_sc_hd` (Sky130nm Foundry Standard Cell High Density)  
│   │   │  ├── libs.tech -> files specific for the tool (klayout,netgen,magic...) 
```

**Synthesis in Openlane:**

Go to VSD Virtual Box and run the following commands:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
```


![asic1](https://github.com/user-attachments/assets/3b4e36c2-6e98-4fb2-8e78-a4ba94f3bb45)

![asic3](https://github.com/user-attachments/assets/358982df-cd58-477b-9b0c-28d9d0cdb106)

![asic2](https://github.com/user-attachments/assets/0abb26fe-6695-40d0-8544-5e9916fe9c2f)

To view the netlist:

```
cd designs/picorv32a/runs/12-11_20-18/results/synthesis/
gedit picorv32a.synthesis.v
```
![asic4](https://github.com/user-attachments/assets/2b547b91-7f39-4d7f-9580-b9225cae3275)
Netlist code:
![asic5](https://github.com/user-attachments/assets/7cd6f0ea-7818-46c7-9dc4-b19dbf6c678b)
![asic6](https://github.com/user-attachments/assets/67dedd74-265e-46c2-bdbf-0796b6ef0095)

To view the yosys report:

```
cd ../..
cd reports/synthesis
gedit 1-yosys_4.stat.rpt
```
![asic8](https://github.com/user-attachments/assets/9f714e19-98a8-4716-b7a3-677da3457981)

![asic7](https://github.com/user-attachments/assets/b2b4779e-da33-45e3-b45d-6698cc31fb91)


Report:

```
28. Printing statistics.

=== picorv32a ===

   Number of wires:              14596
   Number of wire bits:          14978
   Number of public wires:        1565
   Number of public wire bits:    1947
   Number of memories:               0
   Number of memory bits:            0
   Number of processes:              0
   Number of cells:              14876
     sky130_fd_sc_hd__a2111o_2       1
     sky130_fd_sc_hd__a211o_2       35
     sky130_fd_sc_hd__a211oi_2      60
     sky130_fd_sc_hd__a21bo_2      149
     sky130_fd_sc_hd__a21boi_2       8
     sky130_fd_sc_hd__a21o_2        57
     sky130_fd_sc_hd__a21oi_2      244
     sky130_fd_sc_hd__a221o_2       86
     sky130_fd_sc_hd__a22o_2      1013
     sky130_fd_sc_hd__a2bb2o_2    1748
     sky130_fd_sc_hd__a2bb2oi_2     81
     sky130_fd_sc_hd__a311o_2        2
     sky130_fd_sc_hd__a31o_2        49
     sky130_fd_sc_hd__a31oi_2        7
     sky130_fd_sc_hd__a32o_2        46
     sky130_fd_sc_hd__a41o_2         1
     sky130_fd_sc_hd__and2_2       157
     sky130_fd_sc_hd__and3_2        58
     sky130_fd_sc_hd__and4_2       345
     sky130_fd_sc_hd__and4b_2        1
     sky130_fd_sc_hd__buf_1       1656
     sky130_fd_sc_hd__buf_2          8
     sky130_fd_sc_hd__conb_1        42
     sky130_fd_sc_hd__dfxtp_2     1613
     sky130_fd_sc_hd__inv_2       1615
     sky130_fd_sc_hd__mux2_1      1224
     sky130_fd_sc_hd__mux2_2         2
     sky130_fd_sc_hd__mux4_1       221
     sky130_fd_sc_hd__nand2_2       78
     sky130_fd_sc_hd__nor2_2       524
     sky130_fd_sc_hd__nor2b_2        1
     sky130_fd_sc_hd__nor3_2        42
     sky130_fd_sc_hd__nor4_2         1
     sky130_fd_sc_hd__o2111a_2       2
     sky130_fd_sc_hd__o211a_2       69
     sky130_fd_sc_hd__o211ai_2       6
     sky130_fd_sc_hd__o21a_2        54
     sky130_fd_sc_hd__o21ai_2      141
     sky130_fd_sc_hd__o21ba_2      209
     sky130_fd_sc_hd__o21bai_2       1
     sky130_fd_sc_hd__o221a_2      204
     sky130_fd_sc_hd__o221ai_2       7
     sky130_fd_sc_hd__o22a_2      1312
     sky130_fd_sc_hd__o22ai_2       59
     sky130_fd_sc_hd__o2bb2a_2     119
     sky130_fd_sc_hd__o2bb2ai_2     92
     sky130_fd_sc_hd__o311a_2        8
     sky130_fd_sc_hd__o31a_2        19
     sky130_fd_sc_hd__o31ai_2        1
     sky130_fd_sc_hd__o32a_2       109
     sky130_fd_sc_hd__o41a_2         2
     sky130_fd_sc_hd__or2_2       1088
     sky130_fd_sc_hd__or2b_2        25
     sky130_fd_sc_hd__or3_2         68
     sky130_fd_sc_hd__or3b_2         5
     sky130_fd_sc_hd__or4_2         93
     sky130_fd_sc_hd__or4b_2         6
     sky130_fd_sc_hd__or4bb_2        2

   Chip area for module '\picorv32a': 147712.918400
```

```
Flop ratio = Number of D Flip flops = 1613  = 0.1084
             ______________________   _____
             Total Number of cells    14876
```


#### Day-2: Good floorplan vs bad floorplan and introduction to library cells

**Utilization Factor and Aspect Ratio**: In IC floor planning, utilization factor and aspect ratio are key parameters. The utilization factor is the ratio of the area occupied by the netlist to the total core area. While a perfect utilization of 1 (100%) is ideal, practical designs target a factor of 0.5 to 0.6 to allow space for buffer zones, routing channels, and future adjustments. The aspect ratio, defined as height divided by width, indicates the chip’s shape; an aspect ratio of 1 denotes a square, while other values result in a rectangular layout. The aspect ratio is chosen based on functional, packaging, and manufacturing needs.

```
Utilisation Factor =  Area occupied by netlist
                     __________________________
                         Total area of core
                         

Aspect Ratio =  Height
               ________
                Width
```

**Pre-placed cells** : Pre-placed cells are essential functional blocks, such as memory, custom processors, and analog circuits, positioned manually in fixed locations. These blocks are crucial for the chip’s performance and remain fixed during placement and routing to preserve their functionality and layout integrity.

**Decoupling Capacitors** : Decoupling capacitors are placed near logic circuits to stabilize power supply voltages during transient events. Acting as local energy reserves, they help reduce voltage fluctuations, crosstalk, and electromagnetic interference (EMI), ensuring reliable power delivery to sensitive circuits.

**Power Planning**: A robust power planning strategy includes creating a power and ground mesh to distribute VDD and VSS evenly across the chip. This setup ensures stable power delivery, minimizes voltage drops, and improves overall efficiency. Multiple power and ground points reduce the risk of instability and voltage drop issues, supporting the design’s power needs effectively.

**Pin Placement**: Pin placement (I/O planning) is crucial for functionality and reliability. Strategic pin assignment minimizes signal degradation, preserves data integrity, and helps manage heat dissipation. Proper positioning of power and ground pins supports thermal management and enhances signal strength, contributing to overall system stability and manufacturability.

Floorplaning using OpenLANE:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
```

```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
run_synthesis
run_floorplan
```
![asic9](https://github.com/user-attachments/assets/3090eb06-db92-4ba1-ba28-3d74d7bd717d)

![asic10](https://github.com/user-attachments/assets/b7d51e85-fb40-4072-8cd1-75db0132ba60)


Now, run the below commands in a new terminal:

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-11_20-33/results/floorplan
gedit picorv32a.floorplan.def
```
![asic11](https://github.com/user-attachments/assets/197f066d-896c-4555-a492-7d0f96d51c21)

![asic12](https://github.com/user-attachments/assets/2ea7a161-5ee3-4f2a-9169-01ec1ca63592)

According to floorplan definition:

1000 Unit Distance = 1 Micron  

Die width in unit distance = 660685−0 = 660685 

Die height in unit distance = 671405−0 = 671405  

Distance in microns = Value in Unit Distance/1000  

​Die width in microns = 660685/1000 = 660.685 Microns  

Die height in microns = 671405/1000 = 671.405 Microns  

Area of die in microns = 660.685 × 671.405 = 443587.212425 Square Microns

To view the floorplan in magic. Open a new terminal and run the below commands:

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-11_20-33/results/floorplan/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
```

Decap and Tap Cells,Unplaces standard cells at origin
![asic13](https://github.com/user-attachments/assets/42b9a94f-8bb6-49e3-8a8e-d644cb074a6b)
![asic14](https://github.com/user-attachments/assets/71c11aef-d16d-4ee8-ba5a-5569c07d1220)
![asic15](https://github.com/user-attachments/assets/92fecff1-6ed7-4825-9918-b9a15fb96917)
![asic16](https://github.com/user-attachments/assets/b557d577-8c9c-4856-853b-190b2ad573f4)

Command to run placement:

```
run_placement
```
![asic18](https://github.com/user-attachments/assets/8985f68b-63b5-42d2-817b-bef8f9f63683)
![asic19](https://github.com/user-attachments/assets/4879e236-aa3c-4f81-8d71-6d973c573280)

To view the placement in magic:
```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/12-11_20-33/results/placement/
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```
![asic21](https://github.com/user-attachments/assets/3c9e9c7d-16b9-464b-bb64-3f73c3a29335)
![asic20](https://github.com/user-attachments/assets/a871e98c-6192-44f3-a43f-802b9da52e26)
![asic24](https://github.com/user-attachments/assets/d8d5c15e-c464-4b65-9e52-a7eea7d6b057)


**Cell design and Characterization Flow**

Library is a place where we get information about every cell. It has differents cells with different size, functionality,threshold voltages. There is a typical cell design flow steps.

Inputs : PDKS(process design kit) : DRC & LVS, SPICE Models, library & user-defined specs.
Design Steps :Circuit design, Layout design (Art of layout Euler's path and stick diagram), Extraction of parasitics, Characterization (timing, noise, power).
Outputs: CDL (circuit description language), LEF, GDSII, extracted SPICE netlist (.cir), timing, noise and power .lib files

**Standard Cell Characterization Flow**

A typical standard cell characterization flow that is followed in the industry includes the following steps:

- Read in the models and tech files
- Read extracted spice Netlist
- Recognise behavior of the cells
- Read the subcircuits
- Attach power sources
- Apply stimulus to characterization setup
- Provide neccesary output capacitance loads
- Provide neccesary simulation commands
- Now all these 8 steps are fed in together as a configuration file to a characterization software called GUNA. This software generates timing, noise, power models. These .libs are classified as Timing characterization, power characterization and noise characterization.

**Timing parameters**

| Timing definition | Value |
|---|---|
| slew_low_rise_thr | 20% value |
| slew_high_rise_thr | 80% value |
| slew_low_fall_thr | 20% value |
| slew_high_fall_thr | 80% value |
| in_rise_thr | 50% value |
| in_fall_thr | 50% value |
| out_rise_thr | 50% value |
| out_fall_thr | 50% value |
**Propagation Delay**: It refers to the time it takes for a change in an input signal to reach 50% of its final value to produce a corresponding change in the output signal to reach 50% of its final value of a digital circuit.

```
rise delay =  time(out_fall_thr) - time(in_rise_thr)
```

**Transistion time**: The time it takes the signal to move between states is the transition time , where the time is measured between 10% and 90% or 20% to 80% of the signal levels.

```
Fall transition time: time(slew_high_fall_thr) - time(slew_low_fall_thr)
Rise transition time: time(slew_high_rise_thr) - time(slew_low_rise_thr)
```

#### Day-3: Design Library Cell Using Magic Layout and Cell characterization

```
cd Desktop/work/tools/openlane_working_dir/openlane
git clone https://github.com/nickson-jose/vsdstdcelldesign
cd vsdstdcelldesign
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .
ls
magic -T sky130A.tech sky130_inv.mag &
```

![asic22](https://github.com/user-attachments/assets/df726da8-f6a6-41d0-90d4-6e39f7d68522)
![asic23](https://github.com/user-attachments/assets/abf375ea-5ab6-4839-8fc1-df85d1dd5bd0)

Inverter layout:

Identify PMOS:

![asic25](https://github.com/user-attachments/assets/caa64a29-b208-4964-a182-33fa41dea9a1)


Identify NMOS:
![asic26](https://github.com/user-attachments/assets/e52ae2c2-e1af-40f7-a373-3a0383540b36)

Output Y:
![asic27](https://github.com/user-attachments/assets/9d8cc8f9-89c5-4cb4-b987-28e02cfd69de)

PMOS source connected to VDD:
![asic28](https://github.com/user-attachments/assets/09f9d3c8-7a69-4b15-a111-3df43f91ed0f)

NMOS source connected to VSS:
![asic29](https://github.com/user-attachments/assets/a36daa45-f551-4ece-aa59-560e59aa7830)

Spice extraction of inverter in Magic. Run these in the tkcon window:

```
pwd
extract all
ext2spice cthresh 0 rthresh 0
ext2spice
```

```
gedit sky130_inv.spice 
```
![asic30](https://github.com/user-attachments/assets/35a76bdf-bdd8-43ac-9d38-92767c98c361)

![asic31](https://github.com/user-attachments/assets/5f69041c-2d0d-4794-ba1f-9283a5c3b2d6)

Modified `sky130_inv.spice` :
![asic32](https://github.com/user-attachments/assets/f1269a43-c87c-465a-8aae-293471182509)

Simulating the spice netlist
```
ngspice sky130_inv.spice
```
![asic33](https://github.com/user-attachments/assets/b0c26239-9f69-4af1-b32c-cdb8c99c847c)

plotting plot y vs time a

```
plot y vs time a
```
![asic34](https://github.com/user-attachments/assets/39e561a4-016c-4590-b5b3-7b8d8845f85e)

Using this transient response, we will now characterize the cell's slew rate and propagation delay:

Rise Transition: Time taken for the output to rise from 20% to 80% of max value
**Rise transition time calculation**
	Rise Transition Time  = Time taken for output to rise to 80% − Time taken for output to rise to 20%
	20% of output (3.3V) = 0.66V
	80% of output (3.3V) = 2.64V
 
20% Screenshots
![asic45](https://github.com/user-attachments/assets/65e7cc34-d862-4f6d-9264-ba43b3d13874)
![asic44](https://github.com/user-attachments/assets/3b4e125e-8a7d-48fd-bf7d-db0e5e4bd905)

80% Screenshots
![asic46](https://github.com/user-attachments/assets/b05a8bf3-14b0-4133-81ec-3be6ecf87fb9)

 
Fall Transition Time  = Time taken for output to fall to 80% − Time taken for output to fall to 20%
	20% of output (3.3V) = 0.66V
	80% of output (3.3V) = 2.64V

 20% Screenshots
 ![asic47](https://github.com/user-attachments/assets/586ca022-8ed8-4d33-b293-47e8854cafa4)

 
 80% Screenshots
 ![asic48](https://github.com/user-attachments/assets/530a731f-acac-4707-8d83-9a7417069c57)


Rise Cell Delay Calculation
	Rise cell delay = Time taken by output to rise to 50% − Time taken by input to fall to 50% 
	50 % of 3.3V = 1.65V 
 50% Screenshots
 ![asic49](https://github.com/user-attachments/assets/eda6860d-42e0-4143-8e71-5deefeb54a32)

 
Fall Cell Delay Calculation
	Fall cell delay = Time taken by output to fall to 50% − Time taken by input to rise to 50% 
	50 % of 3.3V = 1.65V
 50% Screenshots
![asic50](https://github.com/user-attachments/assets/61d3fcc1-3910-4289-b838-cf5aab0503c5)


```
Rise Transition : 2.24638 - 2.18242 =  0.06396 ns = 63.96 ps
Fall Transition : 4.0955 - 4.05536 =  0.0419 ns = 41.9 ps
Cell Rise Delay : 2.21144 - 2.15008 = 0.06136 ns = 61.36 ps
Cell Fall Delay : 4.07807 - 4.05 =0.02 ns = 20 ps
```

Magic Tool options and DRC Rules:

Now, go to home directory and run the below commands:

```
cd
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
tar xfz drc_tests.tgz
cd drc_tests
ls -al
gvim .magicrc
magic -d XR &
```
![asic35](https://github.com/user-attachments/assets/e75d4032-0d8a-4ef5-93b1-b44d3f2511ca)
![asic36](https://github.com/user-attachments/assets/67c092ea-4b73-44ac-abf5-30d3c6461bf4)
 loading the poly file by load poly.mag on tkcon window.
![asic37](https://github.com/user-attachments/assets/8c7f2dc5-4bd6-434c-bbe9-ade97da0266d)
Observation: We can see that Poly.9 is incorrect.

Adding commands in the sky130A.tech:
![asic38](https://github.com/user-attachments/assets/56a0bbf0-5c16-4c9d-8a69-13d0a65e4dae)
![asic39](https://github.com/user-attachments/assets/e191864c-0e61-4a9d-9155-d5b661f523e5)

Run the commands in tkcon window:

```
tech load sky130A.tech
drc check
drc why
```
![asic40](https://github.com/user-attachments/assets/088eb969-cf51-42c1-8cf1-1e42d03eee60)
![asic41](https://github.com/user-attachments/assets/7280c079-7f11-496f-8752-6e35cf5c0243)

#### Day-4: Pre-layout timing analysis and importance of good clock tree


Commands to extract tracks.info file:
```
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign
cd ../../pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd/
less tracks.info
```

![asic42](https://github.com/user-attachments/assets/c7ea1298-f747-407d-91c6-9ef920d68653)
![asic43](https://github.com/user-attachments/assets/508ca31c-d280-4fc6-a111-10dd8066ff0f)

Commands for tkcon window to set grid as tracks of locali layer

```
grid 0.46um 0.34um 0.23um 0.17um
```
![asic60](https://github.com/user-attachments/assets/27fcd530-0dfc-42f5-812f-3fad507c2f2d)




The grids show where the routing for the local-interconnet layer can only happen, the distance of the grid lines are the required pitch of the wire.
![asic61](https://github.com/user-attachments/assets/73b9bcc8-2a8d-4500-8ea0-64de995fa716)


Now, save it by giving a custon name

```
save sky130_yasinv.mag
```
![asic62](https://github.com/user-attachments/assets/8f2ec8be-2201-4b7c-a736-9e1b82b67e7d)



Now, open it by using the following commands:

```
magic -T sky130A.tech sky130_yasinv.mag &
```
![asic63](https://github.com/user-attachments/assets/59c4f34c-4811-415f-b7eb-5b3b17e9c92f)



Now, type the following command in tkcon window:

```
lef write
```
![asic64](https://github.com/user-attachments/assets/e1cd650e-7902-48a7-bb3c-9d143a866163)

![asic65](https://github.com/user-attachments/assets/977caff7-cbc1-4053-852d-d52c96cfb18a)


lef file:
![asic66](https://github.com/user-attachments/assets/3f7807d0-49da-40a8-b4a6-6927b6c395fd)


Commands to copy necessary files to 'picorv32a' design 'src' directory

```
# Copy lef file
cp sky130_yasinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# Copy lib files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

# List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

```
![asic67](https://github.com/user-attachments/assets/7d1994f2-ddd0-45b8-aa3c-42d19917672c)


Modify config.tcl at path:

```
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a
```
Add these lines in config.tcl:
```
set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]
```


Now, run openlane flow synthesis:

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
```

```
./flow.tcl -interactive
package require openlane 0.9
prep -design picorv32a
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs
run_synthesis
```
![asic69](https://github.com/user-attachments/assets/ce192094-ec69-4949-9af3-bdbe507d75f5)
![asic70](https://github.com/user-attachments/assets/919dcc3f-a71c-46ad-8e34-14aa20c79661)

![asic71](https://github.com/user-attachments/assets/551c6332-596a-484e-93ad-5835d51cff79)

![asic72](https://github.com/user-attachments/assets/8173d30c-0795-4da0-9a08-b8e0d9714deb)

 Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
Noting down current design values generated before modifying parameters to improve timing
```
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```
![asic73](https://github.com/user-attachments/assets/290526ce-3b07-4097-8a80-76c43d401b18)
![asic74](https://github.com/user-attachments/assets/8db88b3d-1620-405c-b39c-ceaecc665163)
![asic75](https://github.com/user-attachments/assets/255daffe-1783-42e5-9b2b-a67ea2a6398c)

Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
Now that our custom inverter is properly accepted in synthesis we can now run floorplan using following command:

```
# Now we can run floorplan
run_floorplan
```
![asic76](https://github.com/user-attachments/assets/98c75ccd-84b7-408b-9eaf-8ea30971f9c8)
![asic77](https://github.com/user-attachments/assets/ba3fe8eb-d072-4a39-9f50-650bbe71e2af)

Since we are facing unexpected un-explainable error while using run_floorplan command, we can instead use the following set of commands available based on information from Desktop/work/tools/openlane_working_dir/openlane/scripts/tcl_commands/floorplan.tcl and also based on Floorplan Commands section in Desktop/work/tools/openlane_working_dir/openlane/docs/source/OpenLANE_commands.md
```
# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or
```
![asic78](https://github.com/user-attachments/assets/5a99f773-5767-4c58-a6a7-3e066591d50c)
![asic79](https://github.com/user-attachments/assets/1611a896-a654-4d66-b704-9b538e754af6)
![asic80](https://github.com/user-attachments/assets/58c55727-4936-49c4-ba07-8c7fc4bb7845)

Now that floorplan is done we can do placement using following command
```
# Now we are ready to run placement
run_placement
```
![asic82](https://github.com/user-attachments/assets/940f8d1f-e6c6-4645-b803-0c2d72bc0df0)
![asic81](https://github.com/user-attachments/assets/b66fcd50-a7c0-44fd-af7e-6397acfe3b71)

Commands to load placement def in magic in another terminal:
```
# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/24-03_10-03/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &
```

Screenshots:

![asic83](https://github.com/user-attachments/assets/9b75732a-2634-4b5f-97e8-2625d4c4f7b2)

![asic84](https://github.com/user-attachments/assets/30866b5d-cbb6-4c88-9fdc-90594f3ab09a)

Command for tkcon window to view internal layers of cells
```
expand
```
![asic85](https://github.com/user-attachments/assets/7cb4b49a-5e6f-4733-8011-9c6c708ceb9f)

Post-Synthesis timing analysis with OpenSTA tool.

Since we are having 0 wns after improved timing run we are going to do timing analysis on initial run of synthesis which has lots of violations and no parameters were added to improve timing

Commands to invoke the OpenLANE flow include new lef and perform synthesis

```
# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

# alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
# Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker
```
```
# Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

# Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

![asic86](https://github.com/user-attachments/assets/48dfbc4d-a060-4697-8b05-be69b0b2df00)

Newly created pre_sta.conf for STA analysis in openlane directory

Newly created my_base.sdc for STA analysis in openlane/designs/picorv32a/src directory based on the file openlane/scripts/base.sdc
![asic87](https://github.com/user-attachments/assets/306b200e-8518-4066-bf75-58cbfd7bad0d)

Commands to run STA in another terminal:
```
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```
![asic89](https://github.com/user-attachments/assets/ebfb6eff-56fa-4335-b901-c6b0457f9222)
![asic90](https://github.com/user-attachments/assets/e964e632-1f55-4a17-be91-8f8ffd8af1dd)

Since more fanout is causing more delay we can add parameter to reduce fanout and do synthesis again

```
cd Desktop/work/tools/openlane_working_dir/openlane
docker
./flow.tcl -interactive
# Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a -tag 25-03_18-52 -overwrite

# Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to set new value for SYNTH_MAX_FANOUT
set ::env(SYNTH_MAX_FANOUT) 4

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```
![asic93](https://github.com/user-attachments/assets/eb0d7503-beb4-4994-b575-67d121f2dfdd)

Commands to run STA in another terminal
```
# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Command to invoke OpenSTA tool with script
sta pre_sta.conf
```
![asic95](https://github.com/user-attachments/assets/2a7eb61c-5ba2-404a-9663-0d6e73531bb0)


![asic94](https://github.com/user-attachments/assets/a6b6d10c-2892-48c2-9ca5-f4dc2cbb3871)


Make timing ECO fixes to remove all violations.
Basic timing ECO
NOR gate of drive strength 2 is driving 5 fanouts
![asic96](https://github.com/user-attachments/assets/06d841d9-c6a3-43b2-93b9-0db32347a129)
Run the following commands to optimise timing:
```
report_net -connections _13111_
replace_cell _16171_ sky130_fd_sc_hd__nor3_4
report_checks -fields {net cap slew input_pins} -digits 4
```

![asic98](https://github.com/user-attachments/assets/0ca86d64-df8b-4b90-8cc1-f468460d98ac)

![asic97](https://github.com/user-attachments/assets/c2139010-fe34-479d-861c-846218b0c423)

We can observe that the tns has reduced to -402.19 from -403.54 and wns has reduced to -5.44 from -5.59.

### Generating custom timing report
```
report_checks -from _32389_  -to _32288_ -through _16171_
```
![asic99](https://github.com/user-attachments/assets/e2d2aa94-a39a-4584-a3fe-df3967fae402)
![asic100](https://github.com/user-attachments/assets/a8b8e3d4-a939-43fe-af13-46c45edea77f)
![asic101](https://github.com/user-attachments/assets/9e95eef8-f594-4cc1-9414-1774f5bf9caa)


**Clock tree synthesis TritonCTS and signal integrity**

Clock Tree Synthesis (CTS) techniques vary based on design needs:

- Balanced Tree CTS: Uses a balanced binary-like tree for equal path lengths, minimizing clock skew but with moderate power efficiency.
- H-tree CTS: Employs an "H"-shaped structure, good for large areas and power efficiency.

   ![image](https://github.com/user-attachments/assets/d1b13f19-a87f-41b6-8f29-a4e00a8e7216)

- Star CTS: Distributes the clock from a central point, minimizing skew but requiring more buffers near the source.
- Global-Local CTS: Combines star and tree topologies, with a global tree for clock domains and local trees within domains, balancing global and local timing.
- Mesh CTS: Uses a grid pattern ideal for structured designs, balancing simplicity and skew.
- Adaptive CTS: Dynamically adjusts based on timing and congestion, offering flexibility but with added complexity.

**Crosstalk**

Crosstalk is interference from overlapping electromagnetic fields between adjacent circuits, causing unwanted signals. In VLSI, it can lead to data corruption, timing issues, and higher power consumption. Mitigation strategies include optimized layout and routing, shielding, and clock gating to reduce dynamic power and minimize crosstalk effects.

![image](https://github.com/user-attachments/assets/21df4ac0-57aa-492e-adfa-7e04ce385680)

**Clock Net Shielding**
Clock net shielding prevents glitches by isolating the clock network, using shields connected to VDD or GND that don’t switch. It reduces interference by isolating clocks from other signals, often with dedicated routing layers and clock buffers. Additionally, clock domain isolation helps prevent cross-domain interference, avoiding metastability and maintaining synchronization.

![image](https://github.com/user-attachments/assets/bf85dd84-dc29-4962-877a-ce4f535bab2c)

### Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
Now to insert this updated netlist to PnR flow and we can use write_verilog and overwrite the synthesis netlist but before that we are going to make a copy of the old old netlist
```
# Change from home directory to synthesis results directory
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/

# List contents of the directory
ls

# Copy and rename the netlist
cp picorv32a.synthesis.v picorv32a.synthesis_old.v

# List contents of the directory
ls
```
![asic102](https://github.com/user-attachments/assets/5c7f6611-2d8a-4897-a57d-3b78d33d1d90)

Commands to write verilog
```
# Check syntax
help write_verilog

# Overwriting current synthesis netlist
write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/picorv32a.synthesis.v

# Exit from OpenSTA since timing analysis is done
exit
```

Verified that the netlist is overwritten:
![asic104](https://github.com/user-attachments/assets/a062a06c-b788-4b10-b765-8224d7adc032)

Since we confirmed that netlist is replaced and will be loaded in PnR but since we want to follow up on the earlier 0 violation design we are continuing with the clean design to further stages

Commands load the design and run necessary stages:
```
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

# Follwing commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or

# Now we are ready to run placement
run_placement

# Incase getting error
unset ::env(LIB_CTS)

# With placement done we are now ready to run CTS
run_cts
```
![asic105](https://github.com/user-attachments/assets/2f2e2b1f-1cc1-410a-a84e-8861f25cf64a)
![asic106](https://github.com/user-attachments/assets/18c6a114-5ad5-41a2-83b5-ed08f02fff36)
![asic108](https://github.com/user-attachments/assets/7b3aff16-9e8f-4f8f-8906-d20365281030)
![asic107](https://github.com/user-attachments/assets/9a6b61a2-3b76-498f-be5b-f31fe248778b)

**Setup timing analysis using real clocks**

A real clock in timing analysis accounts for practical factors like clock skew and clock jitter. Clock skew is the difference in arrival times of the clock signal at different parts of the circuit due to physical delays, which affects setup and hold timing margins. Clock jitter is the variability in the clock period caused by power, temperature, and noise fluctuations, leading to uncertainty in clock edge timing. Both factors are crucial for accurate timing analysis, ensuring the design performs reliably in real-world conditions.

![image](https://github.com/user-attachments/assets/3526c927-e1a9-445a-9dae-22bc7e0446c7)

![image](https://github.com/user-attachments/assets/0c766405-5f9b-4700-a4cd-6fd19e9ea6cc)

Now, enter the following commands for Post-CTS OpenROAD timing analysis:

```
openroad
read_lef /openLANE_flow/designs/picorv32a/runs/25-03_18-52/tmp/merged.lef
read_def /openLANE_flow/designs/picorv32a/runs/25-03_18-52/results/cts/picorv32a.cts.def
write_db pico_cts.db
read_db pico_cts.db
read_verilog /openLANE_flow/designs/picorv32a/runs/25-03_18-52/results/synthesis/picorv32a.synthesis_cts.v
read_liberty $::env(LIB_SYNTH_COMPLETE)
link_design picorv32a
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
set_propagated_clock [all_clocks]
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4
exit
```
![asic109](https://github.com/user-attachments/assets/415d33be-435e-4006-8a3d-68d1f4d34664)
![asic110](https://github.com/user-attachments/assets/12725563-d656-4936-9689-92172220c657)
![asic111](https://github.com/user-attachments/assets/542a54ac-f1ec-4d24-9135-4b1e8eda3060)












































 
 










 








 







