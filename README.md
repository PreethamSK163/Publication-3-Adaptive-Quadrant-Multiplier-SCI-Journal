# Sci Journal Paper — Adaptive Quadrant Multiplier with Dynamic Reconfigurable Structure

> A 16-bit reconfigurable binary multiplier using quadrant decomposition and adaptive row bypassing — implemented in two adder configurations (RCA and Hybrid Parallel Prefix) and evaluated across TSMC 180nm and 90nm CMOS technology nodes using Cadence Genus and Innovus.

![Status](https://img.shields.io/badge/Status-SCI%20Journal%20Under%20Review-yellow)
![Type](https://img.shields.io/badge/Type-Research%20Article-blue)
![Tool](https://img.shields.io/badge/Tool-Cadence%20Genus-blue)
![Tool](https://img.shields.io/badge/Tool-Cadence%20Innovus-blue)
![PDK](https://img.shields.io/badge/PDK-TSMC%20180nm%20%2F%2090nm-orange)
![Language](https://img.shields.io/badge/Language-Verilog%20HDL-purple)



## 📄 Publication Details

| Field | Details |
|:---|:---|
| **Title** | Adaptive Quadrant Multiplier with Dynamic Reconfigurable Structure |
| **Status** | Manuscript under review — SCI-indexed journal |
| **Research Centre** | Centre for Nanoelectronics and VLSI Design (CNVD), VIT Chennai |
| **Technology Nodes** | TSMC 180nm and 90nm CMOS |


## 👥 Authors

| Name | Affiliation |
|:---|:---|
| Adhiyamaan | School of Electrical Engineering, VIT Chennai |
| **Preetham SK** | School of Electrical Engineering, VIT Chennai |
| Dr. S. Umadevi | Associate Professor (Senior), CNVD, VIT Chennai |
| Ph.D. Ms. Rekha | Research Scholar, Vit Chennai |



## 🔍 Overview

The demand for multipliers that can operate adaptively across variable bit-widths in edge intelligence and AI applications has created a significant gap in existing fixed-width architectures. Conventional array and Wallace tree multipliers suffer from high power dissipation during partial product accumulation — particularly in DSP applications where approximately 70% of multiplier bits are zero, leading to unnecessary switching activity in always-active adder rows.

This paper presents an **Adaptive Quadrant (AQ) binary multiplier** — a dynamically reconfigurable architecture that supports multiplication for any bit length through a scalable quadrant-level decomposition approach. The design is implemented in two distinct configurations to provide a balanced exploration between area-optimised and speed-optimised implementations.


## 🧠 Problem Addressed

Existing multiplier architectures collectively exhibit these limitations:

- **Fixed bit-width** — Array, Wallace, Dadda, Vedic, and Booth designs are restricted to specific operand sizes, requiring separate hardware for different bit-widths
- **Unnecessary switching activity** — Partial product rows remain active regardless of input bit patterns, causing excessive dynamic power dissipation
- **Non-scalable final accumulation** — Row bypassing techniques are confined to fixed topologies and lack configurable accumulation stages that adapt to variable bit-widths
- **Speed-area tradeoff** — No single existing design simultaneously achieves scalability, power efficiency, and timing performance across technology nodes


## 💡 Proposed Architecture

### 1. Quadrant Decomposition
Each 2^N × 2^N multiplication is decomposed into four independent sub-multiplications. For N=4 (16×16 operation), operand A is split into lower half P and upper half Q; operand B into lower half R and upper half S. Four partial products — F = P×R, G = Q×R, H = P×S, I = Q×S — are computed in parallel using an 8×8 bypassing multiplier as the fundamental building block.

The same 8×8 module is reused across all four quadrant operations — keeping the architecture modular and scalable to higher bit-widths without structural modification.

### 2. Row Bypassing Scheme
The bypassing mechanism detects zero-valued bits in the multiplicand and disables the corresponding partial product rows — directly suppressing unnecessary switching activity and reducing dynamic power consumption while preserving full computational accuracy.

### 3. Two Adder Variants

**AQ1 — Ripple Carry Adder (RCA) with Bypassing:**
Partial products F, G, H, and I are accumulated through four 2^(N-1) bit Ripple Carry Adders. The structured chaining of RCAs guarantees correct carry propagation while maintaining compact, area-efficient hardware implementation. RCA is selected for its minimal routing complexity and lower power consumption — making AQ1 suitable for power-sensitive applications such as wearables and IoT.

**AQ2 — Hybrid Parallel Prefix Adder:**
The same quadrant decomposition structure is retained, but the accumulation stage uses a three-segment hybrid adder combining Han-Carlson, Weinberger, and Ling carry architectures to minimise critical path delay. This reduces carry propagation depth in the partial product accumulation stage — making AQ2 suitable for high-speed applications such as real-time image processing and DSP systems.


## ⚙️ Implementation

| Parameter | Details |
|:---|:---|
| **HDL** | Verilog HDL |
| **Functional Verification** | Cadence® NC Launch |
| **Logic Synthesis** | Cadence® Genus |
| **Physical Design** | Cadence® Innovus |
| **Technology Nodes** | TSMC 180nm and 90nm CMOS |
| **Operand Size** | 16×16 bits (N=4), scalable |
| **Backend Flow** | 6-metal-layer routing configuration |


## 📊 Key Results

### Frontend Synthesis Results (Cadence Genus)

| Metric | AQ1 (180nm) | AQ1 (90nm) | AQ2 (180nm) | AQ2 (90nm) |
|:---|:---|:---|:---|:---|
| **Leaf Cells** | 633 | 718 | 929 | 998 |
| **Area (µm²)** | 19,851 | 6,345 | 30,968 | 9,622 |
| **Power (mW)** | 1.2323 | 0.2039 | 2.4335 | 0.5818 |
| **Propagation Delay (ns)** | 12.876 | 10.448 | 11.434 | 9.163 |
| **Critical Path (ns)** | 0.956 | 0.420 | 0.563 | 0.405 |
| **Slack (ns)** | 3.024 | 5.452 | 4.466 | 6.737 |

### Technology Scaling — AQ1 (180nm → 90nm)

| Metric | Improvement |
|:---|:---|
| Area reduction | 68.04% |
| Power reduction | 83.45% |
| Propagation delay reduction | 18.86% |

### Comparison Against Existing Designs at 90nm

| Parameter | Design_p1 | Design_p2 | AQ1 | AQ2 |
|:---|:---|:---|:---|:---|
| Propagation Delay (ns) | 7.37 | 10.79 | 10.448 | 9.163 |
| Power (mW) | 18.95 | 20.09 | 0.2039 | 0.5818 |
| Area (µm²) | 8,836 | 10,574 | 6,345 | 9,622 |
| PDP (pJ) | 139.67 | 216.78 | 2.13 | 5.329 |

- AQ1 achieves **98.92% lower power** than Design_p1
- AQ1 achieves **98.47% better Power Delay Product** than Design_p1
- AQ1 achieves **28.19% smaller area** than Design_p1

### Backend Results (Cadence Innovus)

| Metric | AQ1 (180nm) | AQ1 (90nm) | AQ2 (180nm) | AQ2 (90nm) |
|:---|:---|:---|:---|:---|
| **Area (µm²)** | 19,851 | 6,345 | 30,968 | 9,622 |
| **Power (mW)** | 1.531 | 0.2341 | 2.9404 | 0.6333 |
| **Propagation Delay (ns)** | 13.813 | 10.714 | 12.194 | 9.802 |
| **Slack (ns)** | 1.832 | 4.984 | 3.345 | 5.911 |

All configurations meet timing constraints post-layout with positive slack values.


## 🎯 Applications

- **DSP Systems** — Scalable MAC units for FIR/IIR filter banks and FFT engines
- **AI Accelerators** — Variable-precision multiply-accumulate for CNN and edge inference
- **5G/6G Baseband** — High-throughput matrix multiplication for massive MIMO processing
- **IoT and Wearables** — Low-power AQ1 configuration for battery-operated devices
- **Cryptographic Hardware** — Scalable modular multiplication


## 🔗 Related Work

| Output | Details |
|:---|:---|
| **SCI Journal** | Manuscript under review |
| **Related Patent** | Indian Patent Application No. 202541080342 (Published September 2025) |
| **Research Supervisor** | Dr. S. Umadevi, CNVD, VIT Chennai |


## 🤝 Connect

| **Author** | Preetham SK |
|:---|:---|
| **Programme** | B.Tech. Electrical and Electronics Engineering, VIT Chennai |
| **LinkedIn** | [linkedin.com/in/preethamsk16](https://www.linkedin.com/in/preethamsk16) |
| **GitHub** | [github.com/PreethamSK163](https://github.com/PreethamSK163) |
| **Portfolio** | [preethamsk163.github.io](https://preethamsk163.github.io) |
| **Email** | preethamsk163@gmail.com |
