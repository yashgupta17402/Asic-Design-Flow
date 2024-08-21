# Asic-Design-Flow
## Table of Contents
- [Assignment 1](#assignment-1)
- [Assignment 2](#assignment-2)
- [Assignment 3](#assignment-3)
- [Assignment 4](#assignment-4)
- [Assignment 5](#assignment-5)
- [Assignment 6](#assignment-6)
- [Assignment 7](#assignment-7)
  
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
![calcuator_comb](https://github.com/user-attachments/assets/501ba612-43a0-40ce-9933-92ca158e39b4)

## Sequential Circuits

### Fibbonacci Series
![FIB_SEQ](https://github.com/user-attachments/assets/c48d2e91-f212-421f-ac48-6ffb106adc15)

###  Free Running Counter
![FREE_COUNTER_SEQ](https://github.com/user-attachments/assets/48f1d7e7-67ab-48e0-a909-b5b8b444a3ae)

 ### Sequential Calculator
 ![SEQ_CAL](https://github.com/user-attachments/assets/542ad0d9-0672-40a1-a1ec-981da9c6654a)

 ## Pipelined Logic

 ### Producing the Pipeline Design
 ![pipe_1](https://github.com/user-attachments/assets/1bd76344-280b-4e48-985a-ab6d6f6eb3fe)

 ### 2 Cycle Calculator
 
![2_cyle_calc](https://github.com/user-attachments/assets/b845f033-ba01-484f-92da-1a16a51f61a8)

![2_cycle_calc_2](https://github.com/user-attachments/assets/fdb857af-87ac-4fda-b26a-b39b37bbc6da)

## Validity

### Validity- Total Distance Calculator

![total_distance_calc_validity](https://github.com/user-attachments/assets/39794969-9d51-47e6-8278-8212fd041e8b)

## Assignment 7
## Implementation of the RISC-V CPU Core

### Program Counter(PC) and next PC Logic


![pc_counter](https://github.com/user-attachments/assets/581e3ddb-083d-40ca-b4d0-34ab196a4048)



### Instruction Fetch


![fetch_code](https://github.com/user-attachments/assets/e27816f5-5915-4f8b-9319-6e6f8eef155e)

### Instruction Decode

![instruction_decode](https://github.com/user-attachments/assets/c8ba41a7-b9c7-4c58-9cc1-e61604c7e5d0)
### Register File Read


![read](https://github.com/user-attachments/assets/67d93833-cf31-4a84-bf30-4be465a3f1b7)

### Arithmetic Logic Unit (ALU)

![alu](https://github.com/user-attachments/assets/64303e3d-9217-4273-8704-e8a5edf37d09)

### Register File Write

![write_register](https://github.com/user-attachments/assets/832144bf-5b5c-443d-b139-115d9ca14a3f)

### Branch instruction
![branch_instruc](https://github.com/user-attachments/assets/a8448934-f17e-4665-b36f-66b62f080ec6)

### Testbench

```bash
*passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9) ;
```

![TEST_BENCH](https://github.com/user-attachments/assets/b3da6065-a0fe-410a-ae56-7695b3976f62)


![TEST_1](https://github.com/user-attachments/assets/95065231-ee52-4aec-bbf8-c697953e7f50)

##  Implementation of Final RISC-V CPU Core 


![day5_1](https://github.com/user-attachments/assets/6ef4438f-e3ba-4d47-b5ca-be96bebee269)



![day5_2](https://github.com/user-attachments/assets/8de87d0c-cac7-4c51-936f-92f7505b201c)


![day5_6](https://github.com/user-attachments/assets/ed66b7ef-787f-44f2-bdf1-29aa3f5cd8c1)


![day5_3](https://github.com/user-attachments/assets/6f7c5730-309d-43af-a07f-b6e6bc2097ff)


![day5_4](https://github.com/user-attachments/assets/8eb1fe0d-0169-43c1-bd5c-86acf26aca17)

![day5_5](https://github.com/user-attachments/assets/8e7da521-5396-4dec-a212-a4fa4cc13a8e)

 








 







