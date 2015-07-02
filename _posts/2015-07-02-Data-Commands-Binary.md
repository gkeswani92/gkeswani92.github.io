---
layout      : post
title       : "How does the processor differentiate data from commands when everything is in binary?"
date        : 2015-07-01 10:46:05
categories  : Computer Science
---

To understand the how the processor differentiates between the data and commands from the instructions that are passed to it, we need to understand some basic terminologies like instructions, opcodes and operands.

**Instructions** to the processor are encoded as binary instruction codes. Each instruction code contains an operation code, or **opcode**, which specifies the operation that needs to be performed. (e.g. add, subtract, move, input, etc.).

It is generally the first few bytes of an instruction and since every processor has its own set of opcodes defined in its architecture, the machine knows exactly what is to be done.

The number of bits allocated for the opcode is determined by how many different instructions the architecture supports. For example: If there are only 4 operations that a processor can perform, we only need 2 bits for the opcode.

In addition to the opcode, many instructions also contain one or more **operands**, which indicate where in registers or memory the data required for the operation is located. For example, and add instruction requires two operands, and a not instruction requires one.


![Opcodes and Operands](/resources/opcode_operand.png)


These operands are generally provided to the processor in the form of an absolute memory location or an **offset** i.e. a relative memory location with respect to a starting point which may differ from processor to processor.

So each instruction contains an opcode, which will consist of an instruction of N bytes which then expects the subsequent M bytes to be data. 

The processor then uses different segments of memory to store this data and commands. When a program is run, the **instruction pointer/code segment register** points to where the code is while the **data segment register** points to where the data is stored. The **stack segment register** points to the stack, which is the area of memory where all the operations are performed.


![Segmentation of Memory](/resources/memory_segmentation.png)


More details about the working of the processor would be a book on its own. What we need to understand is that the processor actually does not know how to differentiate between the code and data when both are in the binary form. It is through the opcodes that we provide and these demarcated areas in memory that the control unit of the processor knows that they needed to be treated differently.