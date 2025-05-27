+++
title = "Parameters"
hascode = true
date = Date(2019, 3, 22)
tags = ["syntax", "code"]
mintoclevel = 2
maxtoclevel = 3
description = "Comprehensive guide to cuLoRADS solver parameters, including rank control, convergence settings, and performance tuning options."
+++

# Parameters

\tableofcontents

## Basic Parameters

cuLoRADS provides users with customizable parameters to fine-tune the solving process according to specific problem requirements (if needed). Below is a detailed description of each parameter:

| **Parameter**   | **Description**                                                                            | **Type** | **Default Value** |
| --------------- | ------------------------------------------------------------------------------------------ | -------- | ----------------- |
| timesLogRank    | Multiplier for the O(log(m)) rank calculation (rank = **timesLogRank** $\times$ log(m)).   | float    | 2.0               |
| phase1Tol       | Tolerance for ending Phase I.                                                              | float    | 1e-3              |
| phase2Tol       | Tolerance for ending Phase II.                                                             | float    | 1e-5              |
| reoptLevel      | How many times of reopt is allowed (>= 0).                                                 | int      | 4                 |
| dyrankLevel     | Increases sensitivity to rank update triggers as it rises (select from 0, 1, 2).           | int      | 2                 |
| enhancementMode | Enhance robustness of the solver and the accuracy of the solution obtained.                | bool     | true              |
| accLevel        | How accurate the subproblems are solved (select from 0, 1, 2, 3, larger -> more accurate). | int      | 1                 |
| initRho         | Initial value for the penalty parameter $\rho$.                                            | float    | $1/ \sqrt n$      |
| rhoMax          | Maximum value for the penalty parameter $\rho$.                                            | float    | 5000.0            |
| ALMRhoFactor    | Multiplier for increasing $\rho$ ($\rho =$ **ALMRhoFactor** $\times$ $\rho$) in ALM.       | float    | 2.0               |
| ADMMRhoFreq     | Frequency of increasing $\rho$ (increased every **ADMMRhoFreq** ADMM iterations).          | int      | 5                 |
| ADMMRhoFactor   | Multiplier for increasing $\rho$ ($\rho =$ **ADMMRhoFactor** $\times$ $\rho$) in ADMM.     | float    | 1.2               |
| heuristicFactor | Heuristic factor applied when switching to Phase II.                                       | float    | 1.0               |
| lbfgsListLength | The number of vectors stored for L-BFGS                                                    | int      | 2                 |
| maxALMIter      | Maximum iteration number for the ADMM algorithm.                                           | int      | 200               |
| maxADMMIter     | Maximum iteration number for the ADMM algorithm.                                           | int      | 10000             |
| timeSecLimit    | Solving time limitation in seconds.                                                        | float    | 40000.0           |
| juliaWarmStart  | Whether run the solver for a few steps then reset it to reduce Julia compilation overhead. | bool     | false             |

For example, to set **`timesLogRank`** to `1.0` and solve a problem, we can execute

```
./bin/cuLoRADS --filePath /PATH/TO/SDPAFILE.dat-s --timesLogRank 1.0
```
* For the details of the reopt technique and the parameter reoptLevel, please refer to [the paper](https://arxiv.org/abs/2407.15049).

* The time reported in the end is **`GPU solving time`**, the evaluation of dual infeasibility is currently on CPU and not included in the reported time.

* Setting **`juliaWarmStart`** to `true` can remove the influence of Julia compilation time when benchmarking.
