# Asic-Design-Flow
## Table of Contents
- [Assignment 1](#assignment-1)
- [Assignment 2](#assignment-2)
  
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

##Assignment 3

#  Identifying Instruction Types

## As the activity suggests, intruction types are being indentified for the instructions provided. The 32bit code is identified to do so. Each instruction type has it's own instruction format. 



**What are instruction formats in RISCV?** 

Instruction formats can be considered as a 'contract' betwwen the assembly language and the hardware where, if the assembly language 'demands' to execute the instruction, the hardware knows exactly what to do with it. Therefore, there exists certain instructions and their respective format for the hardware to understand. They are made up of series of 0s and 1s depending upon their format, which includes the type of operation, location of data, etc.

There exists 6 types of instruction formats in RISCV.

* R type

    + 'R' here stands for register. 
    + This type inculcates all arithmetic and logical operations.
    +  They are used for operations that involve 3 registers.
    +  The format of R-type instructions is consistent and includes fields for specifying two source registers, one destination register, a function code to specify the operation, and an opcode.
    +  Examples: ADD, SUB, OR, XOR, etc.
    +  The instruction format is as follows: 
  
  <img src="imagessessionthree\rtype.png" alt="Step 1.1" width="400"/> <br>
    + funct7 (7 bits): Function code for additional instruction differentiation.
    + rs2 (5 bits): Second source register.
    + rs1 (5 bits): First source register.
    + funct3 (3 bits): Function code for primary instruction differentiation.
    + rd (5 bits): Destination register.
    + opcode (7 bits): Basic operation code for R-type instructions (0110011 for integer operations).
* I type

    + I-type instructions in the RISC-V architecture are used for operations that involve an immediate value along with one or two registers.
    +  These instructions typically perform operations such as arithmetic with immediate values, load operations, and certain branch instructions.
    +  The format of I-type instructions includes fields for a source register, destination register, an immediate value, a function code, and an opcode.
    +  The instruction format is as follows:
  
  <img src="imagessessionthree\itype.png" alt="Step 1.1" width="400"/> <br>
    + immediate (12 bits): Immediate value used for operations.
    + rs1 (5 bits): Source register.
    + funct3 (3 bits): Function code for instruction differentiation.
    + rd (5 bits): Destination register.
    + opcode (7 bits): Basic operation code for I-type instructions.
  
* S Type 
  
    + S-type instructions in the RISC-V architecture are used for store operations, where data is stored from a register into memory.
   + The format of S-type instructions includes fields for two source registers, an immediate value that determines the memory offset, a function code, and an opcode.
   +  The format is as follows: 

  <img src="imagessessionthree\stype.png" alt="Step 1.1" width="400"/> <br>
    + imm[11:5] (7 bits): Upper 7 bits of the immediate value.
    + rs2 (5 bits): Second source register (contains the data to be stored).
    + rs1 (5 bits): First source register (base address register).
    + funct3 (3 bits): Function code for instruction differentiation.
    + imm[4:0] (5 bits): Lower 5 bits of the immediate value.
    + opcode (7 bits): Basic operation code for S-type instructions.

* B Type

    + B-type instructions in the RISC-V architecture are used for conditional branch operations.
    +  These instructions are designed to alter the flow of execution based on comparisons between two registers. 
    +  The format of B-type instructions includes fields for two source registers, an immediate value that determines the branch offset, a function code, and an opcode.
    +  Following is the instruction format:
    
     <img src="imagessessionthree\btype.png" alt="Step 1.1" width="400"/> <br>
    + imm[12] (1 bit): The 12th bit of the immediate value.
    + imm[10:5] (6 bits): The 10th to 5th bits of the immediate value.
    + rs2 (5 bits): Second source register.
    + rs1 (5 bits): First source register.
    + funct3 (3 bits): Function code for instruction differentiation.
    + imm[4:1] (4 bits): The 4th to 1st bits of the immediate value.
    + imm[11] (1 bit): The 11th bit of the immediate value.
    + opcode (7 bits): Basic operation code for B-type instructions

* U Type

    + U-type instructions in the RISC-V architecture are used for operations involving large immediate values, typically for loading upper immediate values or computing addresses.
    +  The format of U-type instructions includes fields for a destination register, a large immediate value, and an opcode.
    +  The instruction format is as follows:
  
     <img src="imagessessionthree\utype.png" alt="Step 1.1" width="400"/> <br>
    + immediate[31:12] (20 bits): The upper 20 bits of the immediate value.
    + rd (5 bits): Destination register.
    + opcode (7 bits): Operation code for U-type instructions.
    + The immediate value is stored in the upper 20 bits of a 32-bit word, with the lower 12 bits set to zero when used in calculations.

* J type
    + J-type instructions in the RISC-V architecture are used for jump operations, allowing for altering the program control flow by jumping to a specified address.
    + These instructions are typically used for unconditional jumps, like calling functions or implementing loops.
    + Following is the instruction format: 
     
    <img src="imagessessionthree\jtype.png" alt="Step 1.1" width="400"/> <br>
    + imm[20] (1 bit): The 20th bit of the immediate value.
    + imm[10:1] (10 bits): The 10th to 1st bits of the immediate value.
    + imm[11] (1 bit): The 11th bit of the immediate value.
    + imm[19:12] (8 bits): The 19th to 12th bits of the immediate value.
    + rd (5 bits): Destination register where the return address is stored.
    + opcode (7 bits): Operation code for J-type instructions.
   
  
  ## Decoding each instruction type provided: 

   1. ``` ADD r1, r2, r3 ```
  
        + Opcode for ADD = 0110011
        + rd = r1 = 00001
        + rs1 = r2 = 00010
        + rs2 = r3 = 00110
        + func3 = 000
        + func7 = 0000000
        + **R Type**
        + 32 Bit Instruction: 0000000_00110_00010_000_00001_0110011
  
   2. ``` SUB r3, r1, r2 ``` 
        + Opcode for SUB = 0110011
        + rd = r3 = 00110
        + rs1 = r1 = 00001
        + rs2 = r2 = 00010
        + func3 = 000
        + func7 = 0100000
        + **R Type**
        + 32 Bit Instruction: 0100000_00010_00001_000_00110_0110011
         
   3. ``` AND r2, r1, r3 ```
        + Opcode for AND = 0110011
        + rd = r2 = 00010
        + rs1 = r1 = 00001
        + rs2 = r3 = 00011
        + func3 = 111
        + func7 = 0000000
        + **R Type**
        + 32 Bit Instruction: 0000000_00011_00001_111_00010_0110011
         
    4. ``` OR r8, r2, r5 ```
        + Opcode for OR = 0110011
        + rd = r8 = 01000
        + rs1 = r2 = 00010
        + rs2 = r5 = 00101
        + func3 = 110
        + func7 = 0000000 
        + **R Type**
        + 32 Bit Instruction: 0000000_00101_00010_110_01000_0110011
    5. ``` XOR r8, r1, r4 ```
        + Opcode for XOR = 0110011
        + rd = r8 = 01000
        + rs1 = r1 = 00001
        + rs2 = r4 = 00100
        + func3 = 100
        + func7 = 0000000  
        + **R Type**      
        + 32 Bit Instruction: 0000000_00100_00001_100_01000_0110011
    6. ``` SLT r10, r2, r4 ```
  
        + Opcode for SLT  = 0110011
        + rd = r10 = 01100
        + rs1 = r2 = 00010
        + rs2 = r4 = 00100
        + func3 = 010
        + func7 = 0000000
        + **R Type**
        + 32 Bit Instruction: 0000000_00100_00010_010_01100_0110011
  
   4. ``` ADDI r12, r3, 5 ``` 
        + Opcode for ADDI = 0010011
        + rd = r12 = 01100
        + rs1 = r3 = 00110
        + imm[11:0] = 5 = 000000000101
        + func3 = 000
        + **I Type**
        + 32 Bit Instruction: 000000000101_00001_000_00110_0010011
         
   5. ``` SW r3, r1, 4 ```
        + Opcode for SW = 0100011
        + rs2 = r3 = 00100
        + rs1 = r1 = 00001
        + func3 = 010
        + imm[11:0] = 4 = 000000000100
        + **S Type**
        + 32 Bit Instruction: 0000000_00100_00001_010_0100_0100011
    6. ``` SRL r16, r11, r2 ```
        + Opcode for SRL = 0110011
        + rd = r16 = 10000
        + rs1 = r11 = 01011
        + rs2 = r2 = 00010
        + func3 = 101
        + func7 = 0000000 
        + **R Type**
        + 32 Bit Instruction: 0000000_00010_01011_101_10000_0110011
    7.  ``` BNE r0, r1 , 20 ```
        + Opcode for BNE = 1100011
        
        + rs1 = r0 = 00000
        + rs2 = r1 = 00001
        + func3 = 001
        + imm[12:1] = 20 = 000000010100
        + **B Type**   
        + 32 Bit Instruction: 0_000001_00001_00000_001_1010_0_1100011
    8.  ``` BEQ r0, r0, 15 ```
        + Opcode for BEQ = 1100011
        + rs1 = r0 = 00000
        + rs2 = r0 = 00000
        + Imm[12:1] = 15 = 000000001111
        + func3 = 000
        + **B Type**  
        + 32 Bit Instruction: 0_000000_00000_00000_000_1111_0_1100011
    9.  ``` LW r13, r11, 2 ```
        + Opcode for LW = 0000011
        + rd = r13 = 01101
        + rs1 = r11 = 01011     
        + imm[11:0] = 000000000010
        + func3 = 010
        + **I Type**
        + 32 Bit Instruction: 000000000010_01011_010_01101_00001
    10. ``` SLL r15, r11, r2 ```
        + Opcode for SLL = 0110011
        + rd = r15 = 01111
        + rs1 = r11 = 01011
        + rs2 = r2 = 00010
        + func3 = 001
        + func7 = 0000000
        + **R Type**     
        + 32 Bit Instruction: 0000000_00010_01011_001_01111_0110011
    
    Therefore, the instructions have been matched to their corresponding types and their 32 bit layout has been constructed as per their respective format. 


