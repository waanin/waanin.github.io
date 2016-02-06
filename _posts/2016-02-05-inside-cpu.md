---
layout: post
title:  "Processor Architecture introduction"
date:   2016-02-05 13:48:54
categories: CPU
---

* content
{:toc}



###The Big Picture

<br />

![inside cpu]({{"/css/pics/inside_cpu/big_pic.png"}})

<br />


###CPU Basics

<br />

* The computer’s CPU fetches, decodes, and executes program instructions.

* The two principal parts of the CPU are the datapath and the control unit.

	* The datapath consists of an arithmetic-logic unit and storage units (registers) that are interconnected by a data bus that is also connected to main memory.
	* Various CPU components perform sequenced operations according to signals provided by its control unit. 
	* The control unit determines which actions to carry out according to the values in a program counter register and a status register.


###Clocks

* Every computer contains at least one clock that synchronizes the activities of its components.

* A fixed number of clock cycles are required to carry out each data movement or computational operation.

* The clock frequency, measured in megahertz or gigahertz, determines the speed with which all operations are carried out.

* Typical Intel and typical PIC clocks look like this:
	* 2 GHz clock has a cycle time of 0.5 nanoseconds.
	* 8 MHz clock has a cycle time of 0.125 microseconds.

* One master clock has multiple frequencies used for various parts of the system.


###ISA (Instruction Set Architecture)

* Instruction Set Architecture is the structure of a computer that a machine language programmer (or a compiler) must understand to write a correct (timing independent) program for that machine. 

* ISA is the set of all instructions that the microprocessor can execute

![inside cpu]({{"/css/pics/inside_cpu/isa.png"}})


* The set of instructions executed by a modern processor may include:
	* Data transfer instructions
		* data movement (load, store, push, pop, move, swap - registers)
	* Data operation instructions
		* arithmetic and logical (negate, extend, add, subtract, multiply, divide, and, or, shift)
	* Program control instructions
		* control transfer (jump, call, trap - jump into the operating system, return - from call or trap, conditional branch)


###Instruction Processing

* The datapath based on data transfers required to perform instructions
* A controller causes the right transfers to happen

![inside cpu]({{"/css/pics/inside_cpu/instruction.png"}})


###Instruction Execution

![inside cpu]({{"/css/pics/inside_cpu/instructione.png"}})


###Instruction Formats

In designing an instruction set, consideration is given to:

* Instruction length.
	- Whether short, long, or variable.
* Number of operands.
* Number of addressable registers.
* Memory organization.
	- Whether byte - or word addressable.
* Addressing modes.
	- Choose any or all: direct, indirect or indexed

![inside cpu]({{"/css/pics/inside_cpu/instructionf.png"}})


###Addressing Modes

Instructions can specify many different ways to obtain their data

- data in instruction
- data in register
- address of data in instruction
- address of data in register
- address of data computed from two or more values contained in the instruction and/or registers

>On a RISC machine, arithmetic/logic instructions use only the first two of these ADDRESSING MODES

>On a CISC machine, all addressing modes are generally available to all instructions


###RISC vs. CISC 

* The believe that better performance would be obtained by reducing the number of instruction required to implement a program, lead to design of processors with very complex instructions (CISC)

	>CISC – Complex Instruction Set Computers

* As compiler technologies improved, researchers started to wonder if CISC architectures really delivered better performances than architectures with simpler instruction set

	>RISC – Reduced Instruction Set Computers


![inside cpu]({{"/css/pics/inside_cpu/risc.png"}})


* Addition of two operands from memory, with result written in memory, in RISC and CISC architectures

* Having an operation broken into small instructions (RISC) allows the compiler to optimize the code
	> i.e. between the two LD instructions (memory is slow) the compiler can add some instructions that don’t need memory access

* The CISC instruction has no option but to wait for its operands to come from the memory, potentially delaying other instructions


####RISC Characteristics

- One instruction per cycle
- Register to register operations
- Few, simple addressing modes
- Few, simple instruction formats
- Hardwired design (no microcode)
- Fixed instruction format
- More compile time/effort


###Architecture Implementation

![inside cpu]({{"/css/pics/inside_cpu/archim.png"}})


##uArch


###Pipelining


####What Is Pipelining

- Pipelining doesn’t help latency of single task, it helps throughput of entire workload
- Pipeline rate limited by slowest pipeline stage
- Multiple tasks operating simultaneously
- Potential speedup = Number pipe stages
- Unbalanced lengths of pipe stages reduces speedup
- Time to “fill” pipeline and time to “drain” it reduces speedup


####Instruction-Level Pipelining

- For every clock cycle, one small step is carried out, and the stages are overlapped.

![inside cpu]({{"/css/pics/inside_cpu/pipei.png"}})

	- S1. Fetch instruction.
	- S2. Decode opcode.
	- S3. Calculate effective address of operands.
	- S4. Fetch operands.
	- S5. Execute.
	- S6. Store result.

![inside cpu]({{"/css/pics/inside_cpu/pipei2.png"}})


####The Five Stages of Load

![inside cpu]({{"/css/pics/inside_cpu/fives.png"}})

- Ifetch: Instruction Fetch
	- Fetch the instruction from the Instruction Memory
- Reg/Dec: Registers Fetch  and Instruction Decode
- Exec: Calculate the memory address
- Mem: Read the data from the Data Memory
- Wr: Write the data back to the register file


####Pipeline Hurdles

Limits to pipelining: Hazards prevent next instruction from executing during its designated clock cycle.

* `Structural hazards`: HW cannot support this combination of instructions
	- two different instructions use same h/w in same cycle	
* `Data hazards`: Instruction depends on result of prior instruction still in the pipeline
	- two different instructions use same storage
	- must appear as if the instructions execute in correct order	
* `Control hazards`: Pipelining of branches & other instructions  that change the PC 
	- one instruction affects which instruction is next
* Common solution is to stall the pipeline until the hazard  is resolved, inserting one or more “bubbles” in the pipeline


####Insert “Bubble” into the Pipeline

![inside cpu]({{"/css/pics/inside_cpu/pipeb.png"}})


####Data hazards

![inside cpu]({{"/css/pics/inside_cpu/piped.png"}})

![inside cpu]({{"/css/pics/inside_cpu/piped2.png"}})


###Predict Branch



###Out-of-order execution



###Register renaming




###Superscalar




###Multithreading


>The article is converted from a PPT which was written by me in 2013 used to train our team software engineers.
