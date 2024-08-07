# Asic-Design-Flow

## Assignment 1
markdown
# Compilation and Execution of a Simple C Program

## Step 1: Create a New C Program File

In the Linux environment, create a new C program file using any editor. Here, the leafpad editor is used.

### Code Snippet:
c
#include <stdio.h>

int main() {
    int i, n = 200, sum = 0;
    for (i = 1; i <= n; ) {
        sum = sum + i;
        i= i+1;
    }
    printf("The sum from 1 to %d is %d\n", n, sum);
    return 0;
}
![Screenshot from 2024-08-08 00-57-50](https://github.com/user-attachments/assets/c8577b71-e4f4-4082-82f8-6f1a99ba631d)


Save the program and compile your code in the terminal window using the GCC compiler.


## Step 2: Run the Executable Program

Run the executable program and see the output in the terminal window.

### Output

The picture below represents the C code and its output.

![Screenshot](path/to/your/image2.png)

# RISC-V Compilation of a Simple C Program

## Step 1: Code Snippet
c
#include <stdio.h>

int main() {
    int i, n = 5, sum = 0;
    for (i = 1; i <= n; i++) {
        sum = sum + i;
    }
    printf("The sum from 1 to %d is %d\n", n, sum);
    return 0;
}


Compile the C code on the RISC-V compiler.

![Screenshot](path/to/your/image3.png)

Now create the object file (.o) that is the output of the compiler as shown in the procedure below.

![Screenshot](path/to/your/image4.png)

## Step 2: Run the Executable Program

Run the executable program and see the output in the terminal window.

![Screenshot](path/to/your/image5.png)

### Calculation of Number of Instructions

For the "main" section, we can calculate the number of instructions either by counting each individual instruction or by subtracting the address of the first instruction in the next section with the first instruction of the main section and dividing the difference by 4, since it is a byte-addressable memory, so 4 memory blocks form one instruction.

Example:

No. of instructions in main block = (0x101C0 - 0x10184) / 4 = 0x3C / 4 = 0xF = 15 instructions


![Screenshot](path/to/your/image6.png)

## Step 3: Compile the Code with -Ofast Flag

Compile the code again with the compiler flag set as `-Ofast` and observe the generated assembly code.

![Screenshot](path/to/your/image7.png)
![Screenshot](path/to/your/image8.png)

## Observation

Here we can observe that the number of instructions are reduced to 12 as compared to 15 in the previous case.

- `-O1` is moderate in its code optimization while `-Ofast` is highly aggressive to achieve the highest possible performance.
- `-O1` maintains strict adherence to standards while `-Ofast` may violate some standards to achieve better performance.


Replace the path/to/your/imageX.png with the actual paths to your images. This README provides a clear step-by-step guide with code snippets and observations, suitable for a GitHub repository.
