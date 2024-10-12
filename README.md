# Gillespie-Algorithm

This repository contains both **MATLAB** and **Python** code for simulating simple **Birth-Death (BD)** and **Susceptible-Infected-Recovered (SIR)** processes using the **Gillespie algorithm**.

## Introduction

The Gillespie algorithm is a **stochastic simulation method** used to simulate the time evolution of systems with discrete states, particularly in chemical and biological processes where reactions occur randomly over time. It is an individual-based simulation method, introduced by **Dan Gillespie** in 1976.

The algorithm is widely used in systems biology to model processes like gene expression, protein interactions, and other biochemical processes involving random events. It works by randomly sampling both the time of the next event and the state of the next jump in the system. The expected (deterministic-like) dynamics of the system can be obtained by averaging over a large number of realizations (simulations).

### Supported Models
1. **Birth-Death Process (BD)**
2. **Susceptible-Infected-Recovered (SIR) Model**

## Pseudocode for the Birth-Death Process

Here is the pseudocode for simulating a simple **birth-death process** with a **birth rate (b)** and a **death rate (d)** using the Gillespie algorithm:

```plaintext
1. Initialize parameters:
   N = initial_population   // Initial population size
   t = 0                    // Initial time
   t_end = final_time        // Time until which to run the simulation
   b = birth_rate            // Birth rate (probability of a birth event)
   d = death_rate            // Death rate (probability of a death event)

2. While t < t_end and N > 0:
   a. Calculate total propensity:
      a_birth = b * N        // Propensity for birth
      a_death = d * N        // Propensity for death
      a_total = a_birth + a_death

   b. Generate a random number r1 between 0 and 1:
      r1 = random(0, 1)

   c. Compute time to next event:
      delta_t = (1 / a_total) * log(1 / r1)
      t = t + delta_t        // Update the current time

   d. Generate a second random number r2 between 0 and 1:
      r2 = random(0, 1)

   e. Determine if a birth or death event occurs:
      If r2 < (a_birth / a_total):
         N = N + 1           // Birth event: increase population by 1
      Else:
         N = N - 1           // Death event: decrease population by 1

3. Output the time history of population size N over time t.

4. End simulation when t >= t_end or N = 0 (extinction).
