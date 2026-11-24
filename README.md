# GRASP-BLS

**A Greedy Adaptive and Backtracking Framework for Reducing Emission Costs in Generator Scheduling**

Raharjo, Jangkung · Ikhsan, Rifki R. N. · Yustika, Lindiasari M.  
*International Journal of Technology, 16(6), 2005–2024, 2025*  
[![DOI](https://img.shields.io/badge/DOI-10.14716%2Fijtech.v16i6.7588-blue)](https://doi.org/10.14716/ijtech.v16i6.7588)

GRASP + Backtracking Line Search hybrid for economic–emission dispatch (EED) with unit commitment.

## Abstract

The growing demand for efficient and environmentally sustainable power generation calls for advanced optimization methods to address the economic and emission dispatch (EED) problem. This study introduces a novel hybrid optimization approach, GRASP-BLS, which integrates GRASP for global solution space exploration with BLS for accurate local refinement. The synergy between metaheuristic randomness and gradient-based precision is the main contribution of this work, enabling GRASP-BLS to outperform conventional methods in complex, constrained power dispatch scenarios. In a 4-h test case, GRASP-BLS reduced generation costs by 0.4% and emissions by 22.25% compared with SEA. Extended evaluations over a 24-hour period under two scenarios—Scenario 1 (stable loads) and Scenario 2 (dynamic loads with unit commitment)—show that GRASP-BLS consistently yields superior performance. It achieves 5.64%–9.84% cost savings and 1.72%–4.91% emission reductions, outperforming GSA, GWO, and PSO. Despite slightly higher computation time, GRASP-BLS satisfies all operational constraints, including power balance, generation limits, ramp rates, and unit commitment feasibility. These findings highlight the novelty and practicality of GRASP-BLS as a robust, scalable, and adaptive framework for real-world power system optimization, particularly in environments requiring a balance between economic efficiency and environmental responsibility.

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
