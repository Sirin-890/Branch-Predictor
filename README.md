
#  ChampSim Branch Predictor Project

This repository contains our custom branch predictor implementations integrated into [ChampSim], a trace-based simulator for evaluating branch prediction and cache performance.

---

##  How to Clone and Build



add Trace file and put it in dpc3_tracer

### 1. Replace Branch Predictor File

There are **five `.bpred` files** available, each implementing a different branch prediction technique:

- `sol.bpred`
- `sol_2.bpred`
- `sol_3.bpred`
- `sol_4.bpred`
- `sol_5.bpred`

To test a specific one (e.g., `sol_2`):


### 2. Build the Simulator

Use the build script provided by ChampSim:

```bash
./build_champsim.sh sol_2 no no no no lru 1
```



---

## How to Run Simulations

You can run simulations with trace files using the following command:

```bash
./run_champsim.sh 1 1 ./bin/champsim_tracer ./traces/600.perlbench_s-210B.champsimtrace.xz
```

### Syntax:

```bash
./run_champsim.sh sol_2-no-no-no-no-lru-1core 10 540 403.gcc-16B.champsimtrace.xz
```

## trace file:
 403.gcc-16B.champsimtrace.xz

---

## Evaluation of Branch Predictors

We evaluated all five predictors based on:

- **MPKI** (Misses Per Kilo Instructions)  
- **Accuracy**
- **ROB Stalls** (Reorder Buffer stalls)

| Predictor | MPKI ↓ | Accuracy ↑ | ROB Stall ↓ | Comment                        |
|-----------|--------|------------|-------------|--------------------------------|
| sol    | 1.29 | 99.291  | 112        | Basic predictor                |
| **sol_2** | **2.96**| **98.58** | **69.23**     |  Best trade-off              |
| sol_3     | 5.7    | 97.1     | 41    | Less accurate                  |
| sol_4     | 23 | 88| Moderate    | 11  | least rob but very less accuracy   |
| sol_5     | 1.4  | 99.26    |   107.9      | Basic Predictor   |

 **`sol_2.bpred`** offers the **best trade-off** with:

- **Low MPKI**
- **Very high accuracy (98.58%)**
- **Minimal ROB stalls**

---

##  Project Insight

> While simpler branch predictors like the 1-bit saturating counter and bimodal predictors offer ease of implementation, they fail to capture complex branch behaviors. More sophisticated approaches like Local and Global predictors improve accuracy but still exhibit limitations for certain types of branches. Our Tournament predictor overcomes these limitations by combining multiple prediction schemes and dynamically selecting the most effective one for each branch.

> The impressive **98.58% accuracy** achieved by our implementation justifies the additional complexity compared to simpler predictors. For modern high-performance processors where branch mispredictions can significantly impact performance, the Tournament predictor represents an excellent trade-off between implementation complexity and prediction accuracy.

> As processor designs continue to evolve with deeper pipelines and wider issue widths, sophisticated branch prediction becomes increasingly critical. Our Tournament predictor implementation provides a robust foundation that could be further enhanced in future work by incorporating additional prediction schemes or refining the confidence mechanism.

---


