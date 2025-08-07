Simple Instruction Set Computer (SISC) Project
A complete implementation of a simple instruction set computer designed for ECE:3350 Computer Architecture and Organization course. This project demonstrates fundamental concepts of computer architecture including datapath design, control unit implementation, instruction execution, and memory systems.
Project Overview
The SISC project is implemented in Verilog and consists of three progressive parts:

Part 1: Basic datapath with ALU operations and register file
Part 2: Program counter control, instruction memory, and branch execution
Part 3: Data memory integration and load/store instructions, plus custom programs

Architecture Features
Supported Instructions
Part 1 Instructions (R-type and Immediate)

NOP: No operation
ADD: Register addition
ADD IMM: Add immediate value
SUB: Register subtraction
NOT: Bitwise NOT
OR: Bitwise OR
AND: Bitwise AND
XOR: Bitwise XOR
ROTR: Rotate right
ROTL: Rotate left
SHFR: Shift right
SHFL: Shift left
HLT: Halt execution

Part 2 Instructions (Branch)

Branch instructions with program counter control
Conditional and unconditional branches

Part 3 Instructions (Memory)

LDX: Load from memory (indexed)
LDA: Load from memory (absolute)
STX: Store to memory (indexed)
STA: Store to memory (absolute)

System Components

ALU: Arithmetic Logic Unit with multiple operations
Register File: 32-bit registers with dual read ports
Control Unit: Finite state machine for instruction control
Program Counter: Instruction address management
Instruction Memory: Program storage
Data Memory: Data storage and retrieval
Branch Unit: Branch target calculation
Multiplexers: Data path routing

File Structure
├── alu.v              # Arithmetic Logic Unit
├── br.v               # Branch unit
├── ctrl.v             # Control unit (FSM implementation)
├── dm.v               # Data memory module
├── im.v               # Instruction memory module
├── ir.v               # Instruction register
├── mux4.v             # 4-to-1 multiplexer
├── mux16.v            # 16-to-1 multiplexer
├── mux32.v            # 32-to-1 multiplexer
├── pc.v               # Program counter
├── rf.v               # Register file
├── sisc.v             # Top-level SISC module
├── statreg.v          # Status register
├── sisc_tb_p1.v       # Part 1 testbench
├── sisc_tb_p2.v       # Part 2 testbench
├── sisc_tb_p3.v       # Part 3 testbench
├── imem.data          # Instruction memory data
├── dmem.data          # Data memory data
├── sort_data.data     # Test data for sorting
├── sort_instr.data    # Bubble sort program
├── mult_data.data     # Test data for multiplication
├── mult_instr.data    # Multiplication program
└── work/              # ModelSim compilation directory
Getting Started
Prerequisites

ModelSim (or compatible Verilog simulator)
Basic understanding of Verilog and computer architecture

Running the Simulation

Setup Environment
bash# Change to project directory
cd sisc_project

Compile Verilog Files
tcl# In ModelSim
vlog *.v

Run Simulation
tcl# For Part 1
vsim sisc_tb_p1
run -all

# For Part 2
vsim sisc_tb_p2
run -all

# For Part 3
vsim sisc_tb_p3
run -all


Testing Custom Programs
To test the bubble sort program:

Modify im.v to load sort_instr.data
Modify dm.v to load sort_data.data
Run simulation

To test the multiplication program:

Modify im.v to load mult_instr.data
Modify dm.v to load mult_data.data
Run simulation

Custom Programs
Bubble Sort Algorithm

Input: N integers stored at memory locations 1 through N, with N stored at location 0
Output: Integers sorted in ascending order
Algorithm: Implements bubble sort with nested loops

32-bit Multiplication

Input: Two unsigned 32-bit integers at memory locations 0 and 1
Output: 64-bit product stored at locations 2 (LSB) and 3 (MSB)
Method: Implements multiplication through repeated addition

Memory Data Format
Instruction Memory (imem.data)
// 32-bit hexadecimal instructions (8 hex digits each)
80000000  // Example instruction
// Comments supported with //
Data Memory (dmem.data)
// 32-bit hexadecimal data values
00000005  // Example: decimal 5
FFFFFFFF  // Example: -1 in two's complement
Key Implementation Details
Control Unit States

FETCH: Retrieve instruction from memory
DECODE: Decode instruction and prepare operands
EXECUTE: Perform ALU operation or memory access
MEMORY: Handle load/store operations
WRITEBACK: Update register file

Clock Timing

10ns clock period (100MHz)
Reset active low for first 2 clock cycles
All operations synchronized to positive clock edge

Monitoring Signals
The design includes monitoring of key signals:

IR (Instruction Register)
PC (Program Counter)
R1, R2, R3 (Register contents)
ALU_OP (ALU operation)
Control signals (BR_SEL, PC_WRITE, PC_SEL)

Testing and Verification
Each part includes comprehensive testing:

Part 1: Tests all R-type and immediate instructions
Part 2: Verifies branch operations and program flow
Part 3: Validates load/store operations and custom programs

Use the $monitor statements in the testbenches to observe signal changes and verify correct operation.
