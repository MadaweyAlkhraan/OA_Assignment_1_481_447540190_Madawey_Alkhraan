# My Answers - Assignment 1 (CFLP: VNS vs Gurobi)

**Student Information:**
- **Student ID:** 447540190
- **Student Name:** Madawey Alkhraan
- **Gurobi Version Used:** [ yes] Academic [ ] Free
- **Date Completed:**  10 november 2026

---

## Section A: Solution Quality Analysis (4 marks)

### A.1 (2 marks) - Gap Analysis by Categories

**Analysis of Plot 01:**

[ The large category has the highest median optimality gap (14.45%), followed by medium (13.09%) and small (11.03%). 
 
 Moderate instances have the highest average gap (15.97%), compared with expensive (13.89%) and easy (10.60%). 
 
 The large/moderate category has the highest mean gap (18.41%). These results indicate that both instance size and difficulty affect VNS solution quality. ]

**Specific Observations:**
- Highest median gap size: Large 
- Median gap value: 14.45% 
- Effect of difficulty on gap:  Moderate instances have the highest mean gap (15.97%), while easy instances have the lowest (10.60%).


**Outliers identified:**

[Three notable high-gap observations are Instance 101 (Large/Easy, 28.18%), Instance 116 (Large/Moderate, 28.08%), and Instance 69 (Medium/Moderate, 26.59%).

These unusually high gaps may result from premature convergence, insufficient neighborhood exploration, capacity constraints, or weaknesses in the VNS implementation]

**Interpretation:**

 [Larger instances contain more possible facility configurations and customer assignments, making the search more challenging.

 Moderate instances require balancing facility-opening and assignment costs, which creates competing solutions. VNS may stagnate in local optima because its neighborhood moves do not always explore enough feasible alternatives.]


---

### A.2 (2 marks) - Overall Solution Quality Statistics

**From Excel File (Sheet "All Results"):**

- Total instances analyzed: 144
- Instances with gap < 5%:  2 (1.39%)
- Instances with gap < 10%:  38 (26.39%)
- Mean gap across all instances:  13.49%
- Standard deviation of gap:  5.23%

**Interpretation:**

[The average optimality gap of 13.49% indicates that VNS produces feasible solutions but does not consistently reach near-optimal results. Only 2 out of 144 instances (1.39%) achieved a gap below 5%, while 38 instances (26.39%) achieved a gap below 10%.

 The standard deviation of 5.23 percentage points shows noticeable variation in solution quality across instances. Therefore, the current VNS implementation is computationally useful but requires improvements to achieve more consistent, high-quality solutions.]
---

## Section B: Computational Efficiency Analysis (4 marks)

### B.1 (2 marks) - Time Comparison

**Analysis of Plot 02:**

**Size at which VNS becomes significantly faster:**

[VNS becomes significantly faster for medium and large instances, particularly under moderate and expensive difficulty. For medium/moderate instances, Gurobi takes approximately 16.98 seconds compared with 0.74 seconds for VNS.

 For large/expensive instances, Gurobi takes approximately 69.28 seconds compared with only 1.75 seconds for VNS. These results demonstrate that VNS provides substantial computational savings for challenging problems.]

**Most challenging configurations:**
- For VNS: Large/Expensive (size-difficulty) with time: 1.75 seconds
- For Gurobi: Large/Expensive (size-difficulty) with time: 69.28 seconds

**Detailed Comparison:**

[Across all 144 instances, the average Gurobi execution time is 23.65 seconds, while VNS requires only 1.17 seconds on average. VNS is faster because it explores heuristic neighborhoods without proving global optimality.

 However, Gurobi can be faster for easy instances, where its average runtime is 0.85 seconds compared with 0.86 seconds for VNS. For moderate and expensive problems, VNS provides much larger computational savings, making it suitable for time-sensitive applications. Nevertheless, its faster execution comes at the cost of lower solution quality.]

---

### B.2 (2 marks) - Speedup Analysis

**Analysis of Plot 03:**

**Average speedup factors:**
- Small instances: 11.95x faster
- Medium instances: 18.53x faster
- Large instances:30.59x faster

**Instances where Gurobi is faster (speedup < 1):**

[Gurobi was faster than VNS in 26 out of 144 instances: 10 Small/Easy, 8 Medium/Easy, and 8 Large/Easy instances,  All these cases belong to the easy difficulty category. 

This indicates that Gurobi can solve relatively simple optimization problems very efficiently, sometimes faster than the VNS heuristic.]

**Practical Implications:**

[The average speedup increases from 11.95× for small instances to 30.59× for large instances, suggesting that VNS becomes more computationally attractive as problem size grows.

 This makes VNS useful for time-sensitive applications such as logistics planning and real-time decision-making.

  However, the speed advantage comes with reduced solution quality, so the choice between VNS and Gurobi should consider both execution time and optimality gap.]

---

## Section C: Scalability Analysis (3 marks)

### C.1 (1.5 marks) - Scalability Behavior

**Analysis of Plot 04:**

**VNS Scalability:**

[The average VNS execution time increases gradually as problem size grows.

 It rises from 0.97 seconds for small instances to 1.10 seconds for medium instances and 1.44 seconds for large instances.

  This relatively small increase indicates that VNS maintains low computational time across the tested problem sizes.]

**Gurobi Scalability:**

[Gurobi's average execution time increases from 18.57 seconds for small instances to 23.63 seconds for medium instances and 28.76 seconds for large instances. Its runtime is also strongly influenced by problem difficulty because Gurobi must search for and verify an optimal solution. Expensive instances generally require substantially more computational time than easy instances.]

**Comparison:**

[VNS demonstrates better practical scalability in terms of absolute execution time within the tested instances. Its runtime increases from 0.97 to 1.44 seconds, whereas Gurobi's runtime increases from 18.

57 to 28.76 seconds. VNS explores a limited number of heuristic neighborhoods without proving global optimality, while Gurobi performs exact optimization. 

However, these experiments cover only three problem-size categories, so they do not establish which algorithm has better theoretical asymptotic scalability.]

---

### C.2 (1.5 marks) - Growth Rate and Predictions

**Observed Growth of Average Runtime (from your results):**

| Algorithm | Small | Medium | Large | Small → Medium (×) | Medium → Large (×) |
|---|---:|---:|---:|---:|---:|
| VNS avg time (s) | 0.97 | 1.10 | 1.44 | 1.14 | 1.30 |
| Gurobi avg time (s) | 18.57 | 23.63 | 28.76 | 1.27 | 1.22 |

**Shape of growth in Plot 04:**
- VNS: [ ] Roughly steady [ x] Steadily increasing [ ] Sharply increasing
- Gurobi: [ ] Roughly steady [x ] Steadily increasing [ ] Sharply increasing

**Justification:**

[Both algorithms show increasing execution times as the problem size grows. VNS has growth ratios of 1.14× from small to medium and 1.30× from medium to large, while Gurobi has ratios of 1.27× and 1.22×, respectively.

 These values indicate gradual growth rather than a sharp increase.

  Although VNS shows a slightly higher growth ratio in the second transition, its absolute execution time remains significantly lower than Gurobi's.]

**Rough Prediction for Extra Large Instance (n=50, m=20):**
- Predicted VNS time: 1.87 seconds
- Predicted Gurobi time: 35.01 seconds
- How I computed it (e.g., applying the Medium -> Large ratio again):VNS: 1.4371 × (1.4371 / 1.1045) ≈ 1.87 s. Gurobi: 28.7627 × (28.7627 / 23.6282) ≈ 35.01 s

**Suitability for Very Large Instances:**

[I would recommend VNS for very large problems when obtaining a feasible solution quickly is more important than achieving exact optimality. 

The experimental results demonstrate low execution times and favorable practical scalability. 

However, the average optimality gap of 13.49% indicates that solution quality remains a concern. Therefore, VNS should be improved and evaluated on larger instances before being used for applications requiring highly accurate solutions.]

---

## Section D: Quality-Time Tradeoff Analysis (3 marks)

### D.1 (1.5 marks) - Sweet Spot Identification

**Analysis of Plot 05:**

**Sweet Spot:**

[The results do not show a consistent sweet spot where VNS achieves an optimality gap below 5% while providing substantial time savings. 
Only two instances achieved a gap below 5%. Instance 58 (Medium/Easy) had a gap of 4.01%, with VNS taking 0.16 seconds compared with 0.55 seconds for Gurobi.
 However, Instance 104 (Large/Easy) had a gap of 2.56%, but VNS was slower (1.10 seconds) than Gurobi (0.47 seconds). 
 Therefore, VNS does not consistently provide both high solution quality and faster execution.]

**Time Savings for High-Quality Solutions (gap < 5%):**
- Average VNS time: 0.6323 seconds
- Average Gurobi time: 0.5113 seconds
- Absolute savings: -0.1210 seconds
- Relative savings:-23.67%

**Interpretation:**

[For practitioners, these findings show that faster execution does not always coincide with higher solution quality.

Among the two instances with gaps below 5%, VNS was approximately 23.67% slower than Gurobi on average.

 Therefore, decision-makers should evaluate both optimality gap and runtime rather than assuming that VNS always provides a computational advantage.

  VNS may still be useful for moderate and expensive instances when larger gaps are acceptable, while Gurobi is preferable when proven optimality is essential.]

---

### D.2 (1.5 marks) - Practical Decision Making

**Scenarios Justifying 10-15% Gap:**

1. [Emergency Logistics and Disaster Response: During emergencies, rapid decisions are essential for delivering medical supplies, food, and other critical resources. A 10–15% optimality gap may be acceptable if VNS provides a feasible solution quickly while satisfying capacity constraints. In this situation, reducing response time can be more important than achieving the lowest possible cost.]

2. [Temporary Distribution Planning: Companies may need to establish temporary distribution facilities during seasonal demand peaks, such as major sales events. Since these decisions are short-term, obtaining a feasible solution rapidly may be more useful than spending additional time searching for the exact optimum. A moderate cost increase may be justified by operational flexibility.]

3. [Real-Time Operational Adjustments: Unexpected demand changes, facility failures, or transportation disruptions may require immediate adjustments to logistics operations. VNS can quickly generate alternative feasible facility configurations. In such situations, accepting a 10–15% optimality gap may be reasonable if it allows the company to maintain service continuity and avoid costly delays.]

**Recommendation for Real-World Logistics Company:**

[For a real-world logistics company, I recommend Gurobi for long-term strategic decisions, such as selecting permanent facility locations, because these decisions involve significant financial investments and require high-quality solutions.

 In my experiments, Gurobi achieved proven optimality in all 144 instances, while VNS had an average optimality gap of 13.49%. However, VNS was considerably faster on average (1.17 seconds compared with 23.65 seconds for Gurobi).

  Therefore, VNS is more suitable for time-sensitive operational decisions when approximate solutions are acceptable. A hybrid approach combining VNS for rapid initial solutions and Gurobi for optimality verification could provide a practical balance between speed and solution quality.]

---

## Section E: Algorithm Understanding (3 marks)

### E.1 (1.5 marks) - VNS Neighborhood Structures

**Role of Each Neighborhood:**

**N1 (Open Facility):**

- Purpose: Open an additional closed facility and reassign customers while respecting capacity constraints.
- Contribution: [ ] Intensification [x] Diversification
- Explanation: Opening another facility changes the facility configuration and creates new assignment opportunities, This helps VNS explore alternative solutions beyond the current facility arrangement.


**N2 (Close Facility):**

- Purpose: Close or replace an open facility and adjust customer assignments to maintain feasibility.
- Contribution: [ ] Intensification [x] Diversification
- Explanation: This neighborhood modifies the set of open facilities and explores alternative facility configurations. It may reduce fixed opening costs or lead to a better arrangement of facilities and customer assignments.


**N3 (Swap Facilities):**

- Purpose: Exchange an open facility with a closed facility to explore alternative facility combinations.
- Contribution: [ ] Intensification [x] Diversification
- Explanation: Facility swaps allow the algorithm to move into different regions of the solution space. This can help escape local optima and discover facility configurations with lower total costs.

**N4 (Reassign Clients):**

- Purpose: Reassign customers among currently open facilities to improve allocation costs while maintaining capacity constraints.
- Contribution: [x] Intensification [ ] Diversification
- Explanation: Customer reassignment focuses on improving the current solution without changing the set of open facilities. It searches locally for better customer allocations and reduces assignment costs where possible.

**How They Complement Each Other:**

[N1, N2, and N3 mainly support diversification by changing facility configurations, while N4 supports intensification by improving customer assignments within the current configuration. Together, these neighborhoods allow VNS to explore different regions of the solution space and refine promising solutions. 

This combination helps reduce the risk of getting trapped in local optima and can improve overall solution quality, although the experimental results show that the current implementation still experiences stagnation.]

---

### E.2 (1.5 marks) - Convergence Behavior Analysis

**Selected Convergence Plots:**

**Plot 1:**  
 

[Instance name: 097_cflp_large_easy_fac25_cli65]

- Pattern: [x] Smooth [ ] Multiple jumps
- Description: The VNS convergence curve remains almost constant throughout approximately 100 iterations, with a final optimality gap of 6.8%. No significant improvement is observed during the search.
- What it reveals: The algorithm appears to stagnate, as it does not discover better solutions despite continuing the search. The persistent gap from Gurobi's optimum suggests insufficient neighborhood exploration or ineffective local improvements.

 
**Plot 2:** 

[Instance name: 132_cflp_large_expensive_fac25_cli67]

- Pattern: [ ] Smooth [x] Multiple jumps
- Description: The convergence curve shows two noticeable downward steps during the early iterations, followed by a relatively flat segment. The final optimality gap is 18.8%.
- What it reveals: VNS successfully discovers some improved solutions, but it struggles to continue reducing the cost. The relatively large final gap indicates that the algorithm may become trapped in a local optimum or fail to explore sufficiently diverse neighborhoods.


 
**Plot 3:** 

[Instance name: 045_cflp_small_expensive_fac17_cli65]

- Pattern: [ ] Smooth [x] Multiple jumps
- Description: The convergence curve shows several small downward steps during the search, indicating incremental improvements. The final optimality gap is 7.7%.
- What it reveals: The algorithm successfully discovers better solutions through neighborhood exploration. However, the final cost remains above Gurobi's optimum, showing that VNS improves solution quality without guaranteeing global optimality.


**Role of Shaking Mechanism:**

[The shaking mechanism helps VNS escape local optima by perturbing the current solution and exploring different neighborhoods.

 In Plot 2, the downward steps indicate that the search discovered improved solutions at certain iterations, while Plot 3 demonstrates multiple incremental improvements.

  However, Plot 1 shows prolonged stagnation despite continued iterations. These patterns suggest that shaking can support diversification and improve solution quality, but it does not always lead to successful improvements. 

  Stronger neighborhood exploration and improved acceptance mechanisms could help VNS avoid stagnation and reduce optimality gaps.]

---

## Section F: Critical Reflection (3 marks)

### F.1 (1 mark) - Limitations and Improvements

**Main Limitations of Current VNS Implementation:**

1. High Optimality Gaps: The average optimality gap is 13.49%, with a maximum of 28.18%. This indicates that VNS does not consistently produce near-optimal solutions.

2. Premature Convergence: Many convergence plots show long flat segments, suggesting that VNS often stagnates without finding better solutions.

3. Limited Neighborhood Exploration and Implementation Weaknesses: Capacity constraints restrict feasible moves, and the known VNS implementation bug may negatively affect the search process and solution quality.

**Suggested Improvements:**

1. Fix the VNS Acceptance and Update Mechanisms: Correcting how improved solutions are accepted and how the best solution is updated could prevent the loss of beneficial solutions and reduce optimality gaps.

2. Introduce Adaptive Neighborhood Selection: Prioritizing neighborhoods based on their previous improvement performance could make the search more efficient and help VNS explore promising solutions.

3. Apply Multiple Random Restarts and Better Stopping Criteria: Restarting the algorithm from different initial solutions could help escape local optima and improve solution quality, while appropriate stopping criteria could balance runtime and accuracy.

---

### F.2 (1 mark) - Real-World Deployment Considerations

**Additional Constraints for Real Logistics Company:**

1. [Delivery Time Windows: Customers may require deliveries within specific time intervals. The optimization model should ensure that deliveries meet these deadlines to maintain service quality and customer satisfaction.]

2. [Vehicle and Transportation Capacity: Logistics operations depend on available vehicles and their carrying capacities. Including transportation capacity constraints ensures that assigned deliveries can be completed using the company's actual fleet.]

3. [Demand Uncertainty and Facility Availability: Customer demand may change unexpectedly, and facilities may become temporarily unavailable. Accounting for demand uncertainty and potential disruptions improves the reliability and robustness of logistics decisions.]

**Additional Objectives:**

[In addition to minimizing total cost, a real-world logistics company may aim to minimize delivery time, reduce carbon emissions, maximize customer satisfaction, and improve service reliability.

 These objectives can conflict with cost minimization. For example, opening additional facilities may reduce delivery times but increase fixed operating costs. 
 
 Similarly, environmentally friendly transportation may require additional investment.

  Multi-objective optimization methods, such as weighted objectives or Pareto-based approaches, can help decision-makers evaluate these tradeoffs and select solutions that balance financial, operational, and environmental goals.]

---

### F.3 (1 mark) - Exact Method vs Heuristic in Practice

**Gurobi Optimality Status (from the `gurobi_status` column):**
- Instances solved to proven optimality: 144 out of 144
- Instances stopped at the time limit: 0 out of 144
- Do the time-limit instances share a size/difficulty?
 Not applicable. No instances reached the time limit

**What VNS Gives Up and What It Gains:**

[VNS sacrifices solution accuracy in exchange for faster execution. Across the 144 instances, VNS achieved an average optimality gap of 13.49%, while Gurobi found proven optimal solutions for every instance.

 However, VNS required only 1.17 seconds on average, compared with 23.65 seconds for Gurobi.

 This represents approximately 22.48 seconds saved per instance, or a 95.06% reduction in average runtime. Therefore, VNS provides significant computational savings but does not guarantee optimal solutions.]

**Practical Value of Heuristics:**

[Heuristic algorithms such as VNS are valuable in industrial applications because they can generate feasible solutions quickly, especially for large or time-sensitive optimization problems. 

They are useful in logistics, transportation, and facility planning when immediate decisions are required. However, the observed optimality gaps show that heuristics may produce higher-cost solutions than exact methods. 

Therefore, Gurobi is preferable when guaranteed optimality is essential, while VNS is more suitable when fast approximate solutions are acceptable. 

A hybrid approach combining both methods could provide a practical balance between speed and solution quality.]

---

## Section G: BONUS - VNS Improvement Challenge (+3 marks, optional)

*Leave this section empty if you do not attempt the bonus. See Section 8 of the guide. Your improved notebook (`StudentID_FirstName_LastName_Assignment1_IMPROVED.ipynb`) must be pushed to your repository.*

### G.1 (1 mark) - Bug Identification

**Where is the bug?** (cell / function / line numbers in `Assignment_1.ipynb`):

[Paste the faulty line(s) of code]

**What does the bug do?**

[Describe the specific issue]

**Why does it degrade VNS performance?**

[Explain the effect on the search and link it to the high gaps (>20%) in your results]

---

### G.2 (1 mark) - The Fix

**Corrected code:**

```python
# paste your fixed line(s) here
```

**Why does the fix work and why does it not break the rest of the algorithm?**

[Explanation]

---

### G.3 (1 mark) - Demonstrated Improvement

**Before vs After (same instances):**

| Metric | Original VNS | Improved VNS |
|---|---|---|
| Mean gap (%) | | |
| Std of gap (%) | | |
| Instances with gap < 5% | | |
| Instances with gap > 20% | | |
| Mean VNS time (s) | | |

**Analysis:**

[Discuss the improvement, and any change in running time]

**Improved results files (names in your repository):** ___________

---

## Additional Comments (Optional)

[Any additional observations, challenges faced, or insights gained]

---

## Declaration

I hereby declare that:
- I have completed this assignment independently
- All numerical results are from MY experiments using MY student ID
- All analysis and interpretations are MY own work
- I have not copied results or answers from other students
- I understand the consequences of academic dishonesty

**Signature:** _madawey _________

**Date:** 10 november 2026

---

**END OF MY ANSWERS**
