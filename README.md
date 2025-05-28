# MCPU Control Signals Reference

This document provides a summary of control signals used in the design of a multi-cycle MIPS-compatible processor (MCPU). These signals are essential for orchestrating the datapath elements during each cycle of instruction execution.

---

## Memory Control

| Signal     | Description                          | Values               |
|------------|--------------------------------------|----------------------|
| `IorD`     | Selects memory access target         | 0: Instruction, 1: Data |
| `MemRead`  | Memory read enable                   | 0: Disable, 1: Enable |
| `MemWrite` | Memory write enable                  | 0: Disable, 1: Enable |
| `DatWidth` | Data width for memory access         | 000: Word (32-bit), 010: Halfword, 011: Byte, 110: Signed Halfword, 111: Signed Byte |

---

## Instruction Register & Register File Control

| Signal       | Description                               | Values                                  |
|--------------|-------------------------------------------|-----------------------------------------|
| `IRwrite`    | Instruction register write enable         | 0: Disable, 1: Enable                   |
| `RegDst`     | Selects destination register              | 00: $rt, 01: $rd, 02: $rs, 03: $31      |
| `RegDatSel`  | Data source for register write            | 000: ALUOut, 001: MDR, 010: LO, 011: HI, 100: PC |
| `RegWrite`   | Enables register file write               | 0: Disable, 1: Enable                   |

---

## Immediate Extension

| Signal     | Description                          | Values           |
|------------|--------------------------------------|------------------|
| `EXTmode`  | Immediate value extension mode       | 0: Zero-extend, 1: Sign-extend |

---

## ALU Control

| Signal     | Description                          | Values           |
|------------|--------------------------------------|------------------|
| `ALUsrcA`  | ALU input A selection                | 000: RegA, 001: 0x4, 011: PC, 100: MDR |
| `ALUsrcB`  | ALU input B selection                | 000: RegB, 001: 0x4, 011: SEU, 100: SEU << 2 |
| `ALUop`    | ALU operation code                   | e.g., 00000: AND, 00100: ADD, 01001: MUL, 01111: SRA, 10001: SLTU |
| `ALUctrl`  | Extra control bits                   | [1]=swap operands, [0]=shift src: 0=shamt, 1=$rs |

---

## Branch & Jump Control

| Signal   | Description                          | Values                   |
|----------|--------------------------------------|--------------------------|
| `Branch` | Conditional branch control           | 000: No branch, 100: BEQ, 101: BNE, 010~111: Conditional branches |
| `PCsrc`  | Source for PC update                 | 00: ALU, 01: ALUOut, 10: Jump Addr, 11: Current PC |
| `PCwrite`| Program Counter write enable         | 0: Disable, 1: Enable    |

---

## Control State Machine

| Signal     | Description                          | Values           |
|------------|--------------------------------------|------------------|
| `StateSel` | Next state selection in FSM          | 00: Reset, 01: Instr-decided, 11: State + 1 |
> Note: 8 bits before `StateSel` are reserved and must be set to `xxxxxxxx`.

---

## Usage Note

This control signal reference is designed to assist in both designing and debugging the MCPU’s control logic (e.g., PLA or FSM based controllers). It maps out how each instruction or memory interaction should manipulate the datapath.
