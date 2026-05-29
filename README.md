# Supply Chain Network Optimization

Integer Linear Programming (ILP) multi-modal transportation optimization model using Python (PuLP, Pandas) and Power BI.

### Project Overview
The aim of this project is the optimization of a multi-product logistics network for a cosmetics company handling three product types (cosmetics, skincare, haircare) across four transportation modes (Air, Rail, Road, Sea). The network connects suppliers in 5 cities to 3 distribution centers. 

* **Objective:** Minimize total transportation cost and transit time using a weighted objective function (70% cost / 30% time).
* **Model Inputs:** Network optimization is driven by supply data (by city and product), demand data (by DC and product), and lane-mode capacity boundaries derived directly from historical shipment data.

---

### Project Phases & Methodology

## 1. Uncapacitated Baseline Model
* **Approach:** Modeled with basic supply and demand constraints, but without capacity limits, to establish the maximum possible cost and time improvement to set a network benchmark. 
* **Constraint Adjustment:** Because the overall demand for skincare products exceeded the available supply, the constraint for that specific product type was adjusted so that the shipped amount variable for skincare was exactly equal to supply, while standard supply and demand constraints were applied to the other products.
* **Result:** Optimization resulted in a 50.21% reduction in transportation cost and a 30.91% improvement in average transit time. As an unconstrained model, this is not applicable to a real-world scenario; this improvement serves strictly as a baseline benchmark representing the theoretical limit under an ideal scenario.

## 2. Historical Capacity Constraints
* **Approach:** Applied strict historical lane-mode capacity boundaries derived from actual shipment data.
* **Result:** The model returned an infeasible solution. After carrying out a root-cause analysis in Power BI, it was determined that a specific lane (Bangalore - DC_B - Sea) was heavily overloaded, violating its capacity constraint. This proved that the network mathematically cannot satisfy demand and minimize costs while restricted to strict historical capacity limits.

![Phase 2 Bangalore Bottleneck](Lane%20Capacity%20Violation.png)

## 3. Capacity Buffer & Sensitivity Analysis
* **Approach:** Conducted a sensitivity analysis on the lane capacity constraints to identify the minimum capacity expansion required to achieve a feasible solution and optimized transportation network.
* **Result:** Identified that adding a 7% capacity buffer (a 1.07 multiplier) resolves the network bottleneck and enables an optimal solution. This model delivered a 2.58% savings in total shipping cost and a 2.59% improvement in average transit time compared to historical data.

![Phase 3 Optimized Modal Shift](Modal%20shift.png)

---

### Key Insights & Operational Takeaways
Visual analysis of the optimized model in Power BI revealed two primary structural improvements:

* **Strategic Modal Shift:** Volume shifted toward road transportation by 6% (where the majority of products were allocated) and rail transportation by 6.5%, displacing slower, higher-cost alternative modes.
* **Network Consolidation:** Reduced active transportation lanes from 78 historical routes down to 58 optimized routes while fully satisfying network demand. This indicates a potential reduction in administrative and operational overhead, implying further potential cost savings.
