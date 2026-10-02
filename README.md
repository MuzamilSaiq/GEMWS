
# GEMWS
### A Greedy Exchange Method for Warehouse Slotting

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23096290.svg)](https://doi.org/10.5281/zenodo.23096290)

**Author:** Muzamil Saiq  
**Institution:** Florida Institute of Technology  
**Published:** October 1, 2026  
**Status:** Research Preprint  
**DOI:** [10.5281/zenodo.23096290](https://doi.org/10.5281/zenodo.23096290)

---

## Overview

The **Greedy Exchange Method for Warehouse Slotting (GEMWS)** is a volume-partitioned optimization algorithm designed to improve SKU allocation between forward-pick and rear-pick warehouse locations.

GEMWS combines two procedures:

1. **Greedy capacity matching:** Identify the smallest compatible forward-pick partition for a selected rear-pick volume class.
2. **Velocity-based greedy exchange:** Iteratively exchange high-velocity rear-pick SKUs with low-velocity forward-pick SKUs.

Under explicitly stated feasibility assumptions, the method guarantees finite termination and an optimal allocation within the selected partition pair.

The formulation operates on existing warehouse locations without modifying the physical warehouse layout.

---

## 1. Mathematical Formulation

### Stage I: Greedy Partition Selection

Forward-pick (FP) and rear-pick (RP) assignments are grouped into discrete volumetric capacity classes.

For each selected rear-pick partition, GEMWS identifies the smallest forward-pick partition whose capacity is at least as large.

The selection rule is:

$$
j = \min\{k : v_{FP,k} \geq v_{RP,\ell}\}
$$

where:

- \(v_{FP,k}\) denotes a forward-pick capacity class.
- \(v_{RP,\ell}\) denotes the selected rear-pick capacity class.
- \(j\) identifies the smallest compatible forward-pick class.

This selection minimizes the required forward-pick capacity class.

Bidirectional exchange feasibility is assumed separately.

### Stage II: Velocity-Based Greedy Exchange

Within the selected partitions, forward-pick assignments are sorted by descending velocity and rear-pick assignments by ascending velocity.

At each iteration, GEMWS compares the highest rear-pick velocity with the lowest forward-pick velocity.

$$
\Delta = r_{\max} - f_{\min}
$$

An exchange occurs if:

$$
\Delta > 0
$$

Following each exchange, the partitions are reordered and the boundary comparison is repeated.

The algorithm terminates when:

$$
r_{\max} \leq f_{\min}
$$

---

## 2. Algorithm

1. Group forward-pick and rear-pick assignments by volumetric capacity.
2. Select a rear-pick partition.
3. Identify its smallest compatible forward-pick partition.
4. Sort forward-pick assignments by descending velocity.
5. Sort rear-pick assignments by ascending velocity.
6. Compare the highest rear-pick velocity with the lowest forward-pick velocity.
7. If the difference is positive, exchange the corresponding SKUs.
8. Restore the sorted order and repeat.
9. Terminate when no improving exchange remains.

Physical location addresses and capacities remain fixed during exchanges.

---

## 3. Mathematical Guarantees

### Finite Termination

Define the objective function as total forward-pick velocity:

$$
\Phi = \sum_{i=1}^{N} f_i
$$

Every accepted exchange strictly increases the objective:

$$
\Phi_{\text{new}}-\Phi_{\text{old}}
= r_{\max}-f_{\min} > 0
$$

Because the number of possible allocations is finite, the algorithm terminates.

### Optimality Within Selected Partitions

At termination:

$$
r_{\max} \leq f_{\min}
$$

Therefore, every SKU remaining in rear pick has a velocity no greater than every SKU in forward pick within the selected partition pair.

Under the stated feasibility assumptions, the forward-pick partition consequently contains the highest-velocity SKUs from the combined partitions.

This maximizes total forward-pick velocity **within the selected partition pair**.

The result does not imply global optimality across all warehouse partitions.

---

## 4. Research Contribution

GEMWS presents a volume-partitioned warehouse re-slotting formulation combining minimum-compatible-capacity selection with numerical-velocity-based greedy exchanges.

The accompanying research note provides:

- A formal mathematical formulation.
- Explicit partition-selection and exchange rules.
- A finite-termination proof.
- An optimality proof under specified feasibility assumptions.
- A characterization of the method's limitations.

The method builds upon established greedy and exchange principles, applying them to a specific warehouse allocation problem.

---

## 5. Assumptions and Limitations

The current formulation assumes:

- Discrete volumetric capacity classes.
- Bidirectionally feasible cross-boundary exchanges.
- Fixed SKU velocities during optimization.
- Equal objective contributions from locations within a selected forward-pick partition.
- Fixed physical locations and assignment counts.
- No relocation costs.

The optimality guarantee applies to the selected pair of partitions.

The current formulation does not establish global warehouse optimality or directly minimize picker travel distance.

Location-specific packing restrictions, interactions across multiple partitions and relocation costs are potential extensions.

---

## 6. Future Research

Potential extensions include:

- Computational comparisons against established slotting heuristics.
- Mixed-integer linear programming benchmarks.
- Location-specific capacity constraints.
- Relocation-budget constraints.
- Optimization across interacting warehouse partitions.
- Evaluation using synthetic warehouse configurations.

These are proposed extensions rather than results established in the current research note.

---

## 7. Paper and Citation

**Saiq, M. (2026).** *A Greedy Exchange Method for Warehouse Slotting (GEMWS).* Zenodo.

https://doi.org/10.5281/zenodo.23096290

### BibTeX

    @misc{saiq2026gemws,
      author = {Saiq, Muzamil},
      title = {A Greedy Exchange Method for Warehouse Slotting (GEMWS)},
      year = {2026},
      publisher = {Zenodo},
      doi = {10.5281/zenodo.23096290},
      url = {https://doi.org/10.5281/zenodo.23096290}
    }

---

## 8. References

1. Saiq, M. (2026). *A Greedy Exchange Method for Warehouse Slotting (GEMWS).* Zenodo.

2. Aase, G. R., & Petersen, C. G. (2022). A decision support system for re-slotting a case pick distribution center. *Open Journal of Business and Management, 10*(4), 1923–1935. https://doi.org/10.4236/ojbm.2022.104099

3. Edmonds, J. (1971). Matroids and the greedy algorithm. *Mathematical Programming, 1*(1), 127–136.

4. Kernighan, B. W., & Lin, S. (1970). An efficient heuristic procedure for partitioning graphs. *Bell System Technical Journal, 49*(2), 291–307.

---

## License

The research manuscript's licensing terms are specified in its Zenodo record.

Any future software implementation may be licensed separately.
