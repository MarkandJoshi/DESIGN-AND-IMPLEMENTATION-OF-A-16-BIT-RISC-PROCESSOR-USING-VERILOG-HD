# 16-bit RISC Processor in Verilog HDL

A behavioral design of a 16-bit Reduced Instruction Set Computer (RISC) processor implemented in Verilog HDL. The processor is based on Harvard architecture with separate instruction and data memory, uses a single-cycle datapath, and supports 13 instructions across three instruction formats. Each module is designed and verified individually, then integrated into a top-level module.

## Architecture

- **Harvard architecture** — separate instruction and data memory
- **Single-cycle datapath** — each instruction executes in one clock cycle
- **16-bit ALU** — performs 8 arithmetic and logical operations
- **8 general-purpose registers** (R0–R7), each 16-bit, with two read ports and one write port
- **16-bit Program Counter** and **16-bit Instruction Register**
- **Flag register** indicating carry and zero status
- **Control Unit** generating all datapath control signals

## Core Components

- **Instruction Memory (IM)** — stores program instructions, fetched by PC address
- **Program Counter (PC)** — holds the address of the next instruction
- **Instruction Decoder** — decodes the opcode and generates control signals
- **Register File** — eight 16-bit general-purpose registers
- **ALU** — arithmetic and logic operations
- **Data Memory (DM)** — accessed by load/store instructions
- **Control Unit** — generates `alu_op`, `jump`, `beq`, `bne`, `mem_read`, `mem_write`, `alu_src`, `reg_dst`, `mem_to_reg`, and `reg_write`
- **Multiplexers** — select between operand sources based on control signals

## Instruction Format

The instruction word is 16 bits wide:

**R-type:** `opcode[15:12] | Rs1[11:9] | Rs2[8:6] | Rd[5:3] | xxx[2:0]`
**I-type:** `opcode[15:12] | Rs1[11:9] | Rd[8:6] | imm[5:0]`
**J-type:** `opcode[15:12] | address[11:0]`

## Instruction Set

| Instruction | Opcode | Description |
|-------------|--------|-------------|
| `lw`   | 0000 | Read from memory |
| `sw`   | 0001 | Write to memory |
| `add`  | 0010 | Rd = Rs1 + Rs2 |
| `sub`  | 0011 | Rd = Rs1 - Rs2 |
| `not`  | 0100 | Rd = ~Rs |
| `sllv` | 0101 | Rd = Rs1 << Rs2 |
| `srlv` | 0110 | Rd = Rs1 >> Rs2 |
| `and`  | 0111 | Rd = Rs1 & Rs2 |
| `or`   | 1000 | Rd = Rs1 \| Rs2 |
| `slt`  | 1001 | Rd = 1 if Rs1 < Rs2 |
| `beq`  | 1011 | Branch if Rs1 == Rs2 (PC = PC+2+offset) |
| `bne`  | 1100 | Branch if Rs1 != Rs2 (PC = PC+2+offset) |
| `j`    | 1101 | Jump to target address |
| `addi` | 1110 | Rd = Rs1 + imm |
| `subi` | 1111 | Rd = Rs1 - imm |

Instructions fall into four categories: data transfer (`lw`, `sw`), arithmetic (`add`, `sub`, `slt`), logical (`and`, `or`, `not`, `sllv`, `srlv`), and branching (`j`, `beq`, `bne`).

## Instruction Cycle

Each instruction completes in a single clock cycle through these stages: instruction fetch, instruction decode, operand fetch, ALU operation, memory access (for load/store), and result writeback.

## Tools

- **Verilog HDL** — design implementation
- **ModelSim** — logical verification and simulation
- **Quartus Altera II** — synthesis and analysis

## Getting Started

### Prerequisites

- ModelSim (or any Verilog simulator)
- Quartus II (for synthesis/RTL view, optional)

### Simulation

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/<repo-name>.git
   cd <repo-name>
   ```
2. Load the design and testbench files into ModelSim.
3. Compile all modules and run the testbench:
   ```tcl
   vlog *.v
   vsim <top_module_tb>
   run -all
   ```
4. Inspect the waveforms for data transfer, arithmetic, logic, branching, and control signal operations.

## Possible Improvements

- Increase the number of supported instructions
- Add pipelining to improve throughput and performance

## Authors

- **Markand Joshi** — Electronics & Communication Department, Nirma University
- **Pankti Hedau** — Electronics & Communication Department, Nirma University

## License

This project is released under the MIT License. See the `LICENSE` file for details.
