## Problem description

This project studies the population dynamics of a citrus agroecosystem through a system of nonlinear ordinary differential equations involving four interacting components:

- **Diaphorina citri** (insect pest / parasite)
- **Plant shoots**
- **Tamarixia radiata** (parasitoid)
- **External stimuli**

The model captures intrinsic growth, nonlinear self-limitation, and cross-species interactions through a generalized interaction matrix. Population dynamics evolve continuously in time, except for **periodic augmentative releases of parasitoids**, which model biological control interventions.

### Periodic parasitoid releases

Parasitoid releases are implemented as **impulsive events** that instantaneously increase the parasitoid population by a fixed amount \( \Delta \) every \( T \) time units, while allowing continuous evolution between releases.

- In **Wolfram Language**, this mechanism is implemented using `WhenEvent`, directly modifying the state during numerical integration.
- In **Python**, the same behavior is reproduced using `scipy.integrate.solve_ivp` together with explicit event handling (via segmented integration or the `scipy-events` package).

This ensures the mathematical equivalence of the impulsive dynamics across both implementations.

### Numerical methods

- The **Wolfram Language version** uses `NDSolve` with an explicit **Runge–Kutta** time integration scheme.
- The **Python version** relies on adaptive Runge–Kutta methods provided by SciPy, with configurable tolerances to balance accuracy and performance.

The resulting population trajectories are computed over a specified time horizon and visualized to analyze the impact of periodic parasitoid augmentation on ecosystem stability.

### References

The modeling approach and biological motivation are inspired by:

> **Stucchi, L., Giménez-Benavides, L., & Galeano, J.**  
> *The role of parasitoids in a nursery–pollinator system: A population dynamics model.*

### Purpose of this repository

- Provide **equivalent implementations** of a hybrid continuous–discrete ecological model in Wolfram Language and Python.
- Demonstrate how **impulsive differential equations** can be faithfully translated between symbolic and numerical environments.
- Serve as a reference for researchers modeling **biological control strategies** using periodic interventions.
