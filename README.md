# Virtualization Overhead Analysis on ARM and x86 Architectures

## Overview

This project presents a comparative study of virtualization overhead on **ARM** and **x86** architectures. The objective was to quantify the performance impact of virtualization across three critical system subsystems:

* CPU Performance
* Disk I/O Performance
* Network Performance

Benchmarks were executed on both **bare-metal** and **virtualized** environments to evaluate the efficiency of modern virtualization technologies and identify subsystem-specific bottlenecks.

---

## Objectives

* Measure CPU, storage, and network performance under virtualization.
* Compare virtualization overhead between ARM and x86 platforms.
* Analyze the impact of hypervisor design, storage virtualization, and NAT-based networking.
* Identify workload types that are most affected by virtualization.

---

## Test Environments

### ARM Platform

* Host OS: macOS (Apple Silicon)
* Hypervisor: UTM (QEMU-based virtualization)
* Guest OS: Ubuntu Linux
* Storage: Raw disk image (.img)
* Network: NAT

### x86 Platform

* Host OS: Ubuntu Linux
* Hypervisor: Oracle VirtualBox
* Guest OS: Ubuntu Linux
* Storage: Dynamically allocated VDI (.vdi)
* Network: NAT

---

## Benchmarking Tools

### CPU

* Sysbench
* stress-ng
* vmstat
* mpstat

### Disk I/O

* FIO
* iostat
* hdparm
* lsblk

### Network

* iPerf3
* ping
* vmstat
* ss

### Automation & Analysis

* Bash
* Python
* NumPy
* Pandas
* Matplotlib
* SciPy

---

## Methodology

### CPU Evaluation

* Single-thread performance
* Multi-thread performance
* Stability analysis
* CPU utilization monitoring

### Disk Evaluation

* Sequential read/write throughput
* Random read/write IOPS
* Mixed workloads (70% read / 30% write)
* fsync performance
* Block-size scaling tests

### Network Evaluation

* TCP throughput
* UDP throughput
* Round-trip latency (RTT)
* Small-message performance
* Parallel stream scalability

Each benchmark was executed multiple times and statistically analyzed to ensure result reliability.

---

## Key Findings

### CPU Performance

* x86 virtualization achieved near-native performance.
* Single-thread overhead on x86 was approximately 2%.
* Multi-thread performance on x86 was statistically indistinguishable from bare metal.
* ARM exhibited higher CPU overhead due to additional virtualization layers and scheduling complexity.

### Disk I/O Performance

* Disk virtualization introduced significantly higher overhead than CPU virtualization.
* Random write workloads suffered the largest degradation.
* x86 write performance was heavily affected by the VirtualBox VDI storage format.
* ARM achieved lower write overhead through the use of raw disk images.

### Network Performance

* Both architectures experienced substantial network overhead.
* TCP throughput decreased by roughly 50% under virtualization.
* Latency increased by approximately 7–8× compared to bare metal.
* NAT-based networking emerged as a major virtualization bottleneck.

---

## ARM vs x86 Summary

| Component              | ARM              | x86                            |
| ---------------------- | ---------------- | ------------------------------ |
| CPU Virtualization     | Higher Overhead  | Near-Native                    |
| Disk Write Performance | Better           | Worse                          |
| fsync Performance      | Faster           | Slower but Stronger Durability |
| Network Performance    | Similar Overhead | Similar Overhead               |
| Scheduling Stability   | Lower            | Higher                         |

---

## Project Structure

```text
project/
├── scripts/
│   ├── cpu/
│   ├── disk/
│   └── network/
├── results/
│   ├── arm/
│   └── x86/
├── analysis/
├── plots/
├── report/
└── README.md
```

---

## Reproducing the Experiments

### CPU Benchmarks

```bash
bash install_deps_cpu.sh
bash cpu_benchmark.sh
```

### Disk Benchmarks

```bash
bash install_deps_disk.sh
bash disk_benchmark.sh
```

### Network Benchmarks

```bash
bash install_deps_network.sh
bash network_benchmark.sh
```

---

## Conclusions

The study demonstrates that modern virtualization platforms provide highly efficient CPU virtualization, particularly on x86 systems with hardware-assisted virtualization support. However, storage and networking remain significant sources of overhead due to abstraction layers, storage translation mechanisms, and NAT-based packet processing.

The results highlight that virtualization is highly suitable for compute-intensive workloads but requires careful optimization for I/O-intensive applications.

---

## Author

Vini Singh Sisodia

Academic Project – Virtualization Performance Analysis and Systems Benchmarking
