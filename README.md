# GRASP-BLS

**A Greedy Adaptive and Backtracking Framework for Reducing Emission Costs in Generator Scheduling**

Raharjo, Jangkung · Ikhsan, Rifki R. N. · Yustika, Lindiasari M.  
*International Journal of Technology, 16(6), 2005–2024, 2025*  
[![DOI](https://img.shields.io/badge/DOI-10.14716%2Fijtech.v16i6.7588-blue)](https://doi.org/10.14716/ijtech.v16i6.7588)

GRASP + Backtracking Line Search hybrid for economic–emission dispatch (EED) with unit commitment.

## Abstract

The growing demand for efficient and environmentally sustainable power generation calls for advanced optimization methods to address the economic and emission dispatch (EED) problem. This study introduces a novel hybrid optimization approach, GRASP-BLS, which integrates GRASP for global solution space exploration with BLS for accurate local refinement. The synergy between metaheuristic randomness and gradient-based precision is the main contribution of this work, enabling GRASP-BLS to outperform conventional methods in complex, constrained power dispatch scenarios. In a 4-h test case, GRASP-BLS reduced generation costs by 0.4% and emissions by 22.25% compared with SEA. Extended evaluations over a 24-hour period under two scenarios—Scenario 1 (stable loads) and Scenario 2 (dynamic loads with unit commitment)—show that GRASP-BLS consistently yields superior performance. It achieves 5.64%–9.84% cost savings and 1.72%–4.91% emission reductions, outperforming GSA, GWO, and PSO. Despite slightly higher computation time, GRASP-BLS satisfies all operational constraints, including power balance, generation limits, ramp rates, and unit commitment feasibility. These findings highlight the novelty and practicality of GRASP-BLS as a robust, scalable, and adaptive framework for real-world power system optimization, particularly in environments requiring a balance between economic efficiency and environmental responsibility.


## Proposed method

GRASP-BLS couples a greedy randomised adaptive search procedure (GRASP) with a backtracking line search (BLS). GRASP builds a good starting dispatch from restricted candidate lists; BLS then refines it along the numerical gradient with an Armijo acceptance rule. Unit commitment is handled separately by selecting a committed subset before dispatch.

### Economic–emission objective

$$Z(\mathbf{P})=w_1\frac{\sum_{i=1}^{N}\left(a_i+b_iP_i+c_iP_i^2\right)}{\varepsilon}+w_2\frac{\sum_{i=1}^{N}\left(d_i+e_iP_i+f_iP_i^2\right)}{10^{6}}+\lambda\left|\sum_{i=1}^{N}P_i-P_D\right|$$

with $\varepsilon=14{,}385$ IDR/USD, $w_1+w_2=1$, and penalty factor $\lambda=10^{6}$.

Constraints:

$$\sum_iP_i=P_D+P_L,\qquad P_i^{\min}\le P_i\le P_i^{\max},\qquad -D_i\le P_i^{t}-P_i^{t-1}\le U_i$$

Unit commitment selects the committed set

$$\mathcal{A}=\{i\mid u_i=1\},\qquad \sum_{i\in\mathcal{A}}P_i^{\max}\ge P_D$$

with all units switched on as fallback if no subset satisfies the demand.

### Construction phase

For each unit, draw a restricted candidate list from the feasible interval,

$$\tau_i=\{P_i\mid P_i^{\min}\le P_i\le P_i^{\max}\},$$

shuffle 100 equispaced candidates, keep the best fraction $\alpha=0.3$, and greedily accept the value minimising the partial objective:

$$P_i^{\text{best}}=\arg\min_{P_i\in\tau_i}Z\!\left([P_1,\dots,P_i,\dots,P_N]\right)$$

### Backtracking line search

Gradient by central differences with $h=10^{-8}$:

$$g_j=\frac{Z(\mathbf{P}+h\mathbf{e}_j)-Z(\mathbf{P}-h\mathbf{e}_j)}{2h}$$

Start with step $s=1$ and accept the first step satisfying the Armijo condition:

$$\mathbf{P}'=\mathbf{P}-s\mathbf{g},\qquad Z(\mathbf{P}')\le Z(\mathbf{P})-\alpha s\|\mathbf{g}\|^2$$

Otherwise shrink $s\leftarrow\beta s$ with $\alpha=0.3$, $\beta=0.8$, until $s<10^{-3}$. The outer loop repeats the gradient step while the iterate keeps changing.

### Feasibility restoration

Ramp limits are enforced as

$$P_i^{t}\leftarrow\min\!\left(P_i^{t-1}+U_i,\;\max\!\left(P_i^{t-1}-D_i,\;P_i^{t}\right)\right),$$

then the residual balance error is spread equally over the units and clipped, iterating until $\left|\sum_iP_i-P_D\right|\le10^{-3}$ MW.

Reported over six 24-hour load levels: cost reductions of 5.64%–9.84% and emission reductions of 1.72%–4.91% against GSA, PSO, GWO, WOA and other baselines.

## Contents

```
.gitignore
GRASP-BLS_EED-UC.ipynb
GRASP-BLS_EED.ipynb
figures/
  LCFD.png
  feasible_area.png
  results_summary.png
load_demand.ipynb
results/
  24-hours/
  24-hours (UC)/
  4-hours/
```

## Data

Input data is **not included**. Place files in `data/` (notebooks) or next to the `.m` script (MATLAB):

| File | Columns |
|---|---|
| `EED8u.xlsx` | Sheet1: `Unit`, `a`, `b`, `c`, `d`, `e`, `f`, `pmin`, `pmax`, `rampdown`, `rampup` |
| `EED_demand8u.xlsx` | Sheet1: `load`, `load2`, `load3` |

## Requirements

Python. Python notebooks: `numpy`, `pandas`, `scipy`, `matplotlib` (as imported). MATLAB scripts: R2021a+.

## Citation

```bibtex
@article{Raharjo_2025, title={A Greedy Adaptive and Backtracking Framework for Reducing Emission Costs in Generator Scheduling}, volume={16}, ISSN={2086-9614}, url={http://dx.doi.org/10.14716/ijtech.v16i6.7588}, DOI={10.14716/ijtech.v16i6.7588}, number={6}, journal={International Journal of Technology}, publisher={International Journal of Technology}, author={Raharjo, Jangkung and Ikhsan, Rifki R. N. and Yustika, Lindiasari M.}, year={2025}, month=Dec, pages={2005} }
```

## License

[![CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](LICENSE)

Licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). **Attribution is required**: any use of this code, results, or figures, including in publications, must cite:

> Jangkung Raharjo; Rifki Rahman Nur Ikhsan; Lindiasari Martha Yustika (2025). A Greedy Adaptive and Backtracking Framework for Reducing Emission Costs in Generator Scheduling. *International Journal of Technology*. https://doi.org/10.14716/ijtech.v16i6.7588
