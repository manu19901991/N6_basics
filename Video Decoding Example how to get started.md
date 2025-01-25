---
title: Video Decoding Example how to get started

---

# Video Decoding Example how to get started

1- Open Benchmark\Projects\STM32N6570-DK
2- Examples contain the real decoding application, FSBL the first stage bootloader implementation

FSBL can be compiled, but has described above, it needs an header to be recognized by the BootROM


'This is a script that uses the signing tool to sign the initial fsbl version '

# Project Setup and FSBL Signing Script

## Steps to Open Project and Compile FSBL

1. Open the following directory in your project: `Benchmark\Projects\STM32N6570-DK`.
2. In this directory, you'll find:
   - **Examples**: Contains the actual decoding application.
   - **FSBL**: The first stage bootloader implementation.

Note: The FSBL can be compiled, but it requires a header to be recognized by the BootROM.

## FSBL Signing Script

This script uses the signing tool to sign the initial FSBL version.
FSBL.bin is the input and Project-trusted.bin is the output

```c
del Project.bin
copy FSBL.bin Project.bin
"C:\Program Files\STMicroelectronics\STM32Cube\STM32CubeProgrammerN6\bin\STM32MP_SigningTool_CLI.exe" -bin FSBL.bin -nk -of 0x80000000 -t fsbl -o Project-trusted.bin
```
Project-trusted.bin is also included in the ftp sent to you.

# Programming Instructions

## openH264.bin Programming

- Select the below loader in external loader list

![image](https://hackmd.io/_uploads/SJFLsYzukx.png)


- The `openH264.bin` file, provided via FTP (or compiled via IAR), must be programmed using Cube Programmer with the board in Developer mode.

### Developer Mode

![Developer Mode](https://hackmd.io/_uploads/SyQPKKzdJx.png)

- It must be programmed at this address: `@0x70100000`.

## Project-trusted.bin Programming

- The `Project-trusted.bin` file must be programmed at this address: `@0x70000000`.

## Post-Programming Steps

- When programming is over, turn the switch board to user mode and power cycle. 
- Red LED2 will be blinking

### User Mode

![User Mode](https://hackmd.io/_uploads/HkxCKFGdyg.png)

## USART Terminal Configuration

- Open a USART Terminal with the following configuration:

![USART Configuration](https://hackmd.io/_uploads/B1gC9KfOyl.png)

Use the following terminal setup

![image](https://hackmd.io/_uploads/Sy541qfukx.png)


You'll get the following output

![image](https://hackmd.io/_uploads/SyCLJcf_1x.png)


Entering the related number, the video is decoded
