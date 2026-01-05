# ALU Simulation Report

## Overview
This project implements a basic ALU supporting:
- ADD
- SUB
- AND
- OR
- NOT

Flags: Zero (Z), Negative (Nf), Carry (C), Overflow (V).

## Simulation Environment
- Tool: Icarus Verilog (`iverilog`)
- Waveform viewer: GTKWave
- Testbench: `tb/tb_alu.v`

## Results

| Opcode | Operation | A         | B         | Y         | Z | Nf | C | V |
|--------|-----------|-----------|-----------|-----------|---|----|---|---|
| 000    | ADD       | 0x00000001| 0x00000001| 0x00000002| 0 | 0  | 0 | 0 |
| 001    | SUB       | 0x00000005| 0x00000003| 0x00000002| 0 | 0  | 1 | 0 |
| 010    | AND       | 0xF0F0F0F0| 0x0F0F0F0F| 0x00000000| 1 | 0  | 0 | 0 |
| 011    | OR        | 0xF0F0F0F0| 0x0F0F0F0F| 0xFFFFFFFF| 0 | 1  | 0 | 0 |
| 100    | NOT       | 0xAAAAAAAA|     —     | 0x55555555| 0 | 0  | 0 | 0 |

## Waveform
The `waves.vcd` file shows correct transitions for all operations.  
Example screenshot (GTKWave):
