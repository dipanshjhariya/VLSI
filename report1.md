# Synchronous RAM Simulation Report

## Overview
This project implements a simple synchronous RAM with:
- 16 memory locations (ADDR_WIDTH = 4)
- 8-bit data width (DATA_WIDTH = 8)
- Synchronous read and write operations

## Simulation Environment
- Tool: Icarus Verilog (`iverilog`)
- Waveform viewer: GTKWave
- Testbench: `tb/tb_ram.v`

## Results

| Time (ns) | WE | Addr | Din | Dout |
|-----------|----|------|-----|------|
| 10        | 1  | 0x0  | 0xAA| 0xAA |
| 20        | 1  | 0x1  | 0x55| 0x55 |
| 30        | 1  | 0x2  | 0xFF| 0xFF |
| 40        | 0  | 0x0  |  —  | 0xAA |
| 50        | 0  | 0x1  |  —  | 0x55 |
| 60        | 0  | 0x2  |  —  | 0xFF |

## Waveform
The `waves.vcd` file shows correct synchronous read/write behavior.

## Conclusion
The RAM module correctly stores and retrieves data on clock edges.  
Design is synthesizable and ready for FPGA/ASIC integration.