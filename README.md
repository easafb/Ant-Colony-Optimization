# Fast Ant Colony Optimization (ACO) for TSP

A lightweight, vectorized Python implementation of the **Ant Colony Optimization (ACO)** metaheuristic designed to solve the **Traveling Salesperson Problem (TSP)** using `NumPy`.

---

## Overview

Ant Colony Optimization simulates the foraging behavior of real ants. By depositing and following pheromone trails with evaporation mechanics, the colony self-organizes to identify near-optimal paths in complex search spaces without central coordination (emergent intelligence).

This implementation replaces nested Python lookups with vectorized array operations and boolean masking, drastically reducing evaluation times compared to standard loop-heavy implementations.

---

## Features

* **Vectorized Probability Engine**: Eliminates slow path-checking loops via NumPy boolean masks.
* **Pre-calculated Heuristics**: Pre-computes visibility matrices ($1 / \text{distance}$) with zero-division protection.
* **Zero External Optimization Dependencies**: Runs directly on pure NumPy without requiring heavy framework setups.

---

## Mathematical Formulation

At step $t$, an ant at node $i$ chooses the next node $j$ according to the probability:

$$P_{ij} = \frac{[\tau_{ij}]^\alpha \cdot [\eta_{ij}]^\beta}{\sum_{k \in \text{unvisited}} [\tau_{ik}]^\alpha \cdot [\eta_{ik}]^\beta}$$

Where:
* $\tau_{ij}$: Pheromone level on edge $(i, j)$
* $\eta_{ij} = \frac{1}{d_{ij}}$: Heuristic visibility (inverse distance)
* $\alpha$: Pheromone influence factor
* $\beta$: Heuristic distance priority factor

Pheromone evaporation occurs globally after each iteration:

$$\tau_{ij} \leftarrow (1 - \rho) \cdot \tau_{ij} + \sum_{k} \Delta \tau_{ij}^k$$

Where $\rho$ is the decay rate and $\Delta \tau_{ij}^k = \frac{1}{L_k}$ for ants traversing edge $(i, j)$.

---

## Getting Started

### Prerequisites

```bash
pip install numpy
