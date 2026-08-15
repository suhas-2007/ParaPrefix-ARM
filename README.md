# ParaPrefix-ARM

## Fused Shift+Add ARM Execute Stage

A Computer Organization & Architecture project that implements an optimized ARM execute stage by combining shift and add operations into a single execution path using Verilog HDL.

## Project Overview

Traditional ARM execute stages can have a long critical path when a barrel shifter and ripple-carry adder are used sequentially. This project proposes a fused architecture using a logarithmic barrel shifter, smart bypass logic, and a Kogge-Stone parallel-prefix adder.

The proposed design aims to reduce the critical-path depth from approximately **35 gate levels to 11 gate levels**.

## Architecture

The execute stage consists of:

* **Logarithmic Barrel Shifter** – Performs shifting using 5 stages for 32-bit data.
* **Smart Path Bypass** – Directly routes `Rm` to the adder when `shift_amt = 0`.
* **Kogge-Stone Adder** – Uses parallel-prefix carry computation for faster addition.
* **Execute Stage** – Integrates the complete datapath.

## ARM Shift+Add Operation

```text
ADD Rd, Rn, Rm, LSL #n

Rd = Rn + (Rm << n)
```

## Main Features

* 32-bit datapath
* Fused Shift + Add execution
* Logarithmic barrel shifter
* Kogge-Stone parallel-prefix adder
* Smart bypass path
* Parameterized Verilog design
* Single-cycle execution path
* RTL simulation and testbench verification

## Project Structure

```text
ParaPrefix-ARM/
│
├── rtl/
│   ├── execute_stage.v
│   ├── log_barrel_shifter.v
│   ├── kogge_stone_adder.v
│   └── smart_path_bypass.v
│
├── testbench/
│   ├── tb_execute_stage.v
│   ├── tb_kogge_stone_adder.v
│   └── tb_log_barrel_shifter.v
│
├── docs/
│   └── COA_Course_Project.pptx
│
└── README.md
```

## Verification

The design was tested using:

* **Icarus Verilog (iverilog)** for simulation
* **GTKWave** for waveform analysis
* RTL testbenches for the execute stage, Kogge-Stone adder, and barrel shifter

The project presentation reports successful assertion checks and verification of the bypass path.

## Reported Results

| Metric                   |           Result |
| ------------------------ | ---------------: |
| Critical-path depth      | ~35 → ~11 levels |
| Gate-depth reduction     |             ~68% |
| Fused throughput         |      2 ops/cycle |
| Bypass usage             |             ~80% |
| Reported CPI improvement |             ~35% |

## Team

* L. Sai Bhupesh — CS24B2029
* R. Suhas — CS24B2040
* N. Sasindra Sri Sai — CS24B2041
* D. Charan Chandu — CS24B2047

## Course

**Computer Organization & Architecture**
**B.Tech CSE — 2025**

## Future Scope

* Integration with a complete 5-stage ARM pipeline
* Support for ASR, ROR and RRX shift operations
* FPGA synthesis and timing analysis
* Exploration in superscalar/out-of-order architectures

## License

This project was developed as part of an academic course project.
