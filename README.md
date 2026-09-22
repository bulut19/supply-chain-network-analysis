# Supply Chain Network Analysis & Optimization

A NetworkX-based approach to modeling multi-echelon inventory systems as graphs, optimizing replenishment flow, running sensitivity analysis, and stress-testing network structure for resilience. Includes a full tutorial plus an original mini case applying the same toolkit to a hype-driven sneaker brand's fulfillment network.

## Overview

Most supply chain analysis treats a network as a set of cost parameters. This project treats it as a graph, with NetworkX handling flow optimization, centrality, and connectivity, so the network's topology itself becomes part of the analysis, not just its costs.

**Part 1: Tutorial**, built around the ALKO case (Chopra & Meindl, *Supply Chain Management*), a two-echelon distribution network (1 plant, 5 regional distribution centers):
- Model the network as a directed graph with inventory policy parameters (EOQ, safety stock, ROP) stored as node/edge attributes
- Solve a minimum-cost flow replenishment problem with `nx.min_cost_flow()`, shown to be equivalent to the underlying transportation linear program
- Run sensitivity analysis on arc capacity, demand variability, and inter-regional demand correlation
- Assess structural vulnerability with degree centrality, a node-removal stress test, and edge connectivity

**Part 2: Mini case ("DropKicks")**, an original scenario applying the same toolkit to a fictional limited-edition sneaker brand allocating a hype-driven drop across 5 regional fulfillment centers, including a stress test simulating a product going viral.

## Key Findings

- **Star topologies have zero redundancy.** In both the ALKO and DropKicks networks, every plant/facility-to-region arc has edge connectivity of exactly 1, a single arc failure cuts off that region entirely, and the $0.0000 shadow price on capacity confirms there's no alternative routing to absorb a shortfall.
- **Demand correlation drives the value of centralization.** As inter-regional demand correlation rises from 0 to 1, the risk-pooling benefit of centralizing inventory shrinks to zero, centralization only pays off when regional demand is independent.
- **Degree centrality flags the single point of failure.** The central plant/facility is structurally the most critical node: its failure disrupts every downstream region simultaneously, while losing any one DC/FC only affects that region.
- **DropKicks stress test:** tripling demand volatility (simulating a viral moment) left shipping costs unchanged (batch sizes are fixed) but nearly tripled required safety stock network-wide (114 to 343 units, +200%), the real risk in a hype-driven network is inventory holding cost, not shipping capacity.

## Tech Stack

Python (NetworkX, matplotlib, NumPy, pandas) · Google Colab

## Repository Contents

- `supply_chain_network_analysis.ipynb`: full tutorial (5 sections: graph modeling, flow optimization, sensitivity analysis, network vulnerability) plus the original DropKicks mini case
- `README.md`: this file
