# FHP-1-Lattice-Gas-Simulation

A C-based implementation of the Lattice Boltzmann Method for computational fluid dynamics, with both serial and parallel (MPI) versions for HPC clusters.

## Overview

This project simulates fluid flow using a **D2Q6 lattice** (2D hexagonal lattice with 6 discrete velocity directions). It includes:

| File | Description |
|------|-------------|
| `proj_serial.c` | Single-threaded reference implementation |
| `proj_parallel.c` | MPI parallel version for distributed memory systems |
| `proj_parallel.sh` | SLURM batch script for cluster job submission |

## Physics Model

### D2Q6 Lattice Structure
Each lattice node has 6 velocity directions (legs) numbered 0–5:


### Simulation Steps
1. **Collision**: Local particle interactions based on conservation laws
   - Head-on collisions (back-to-back particles)
   - Three-particle symmetric collisions
   - Four-particle collisions
2. **Streaming**: Particle propagation to neighboring nodes
3. **Boundary Conditions**:
   - **Inflow** (top): Dirichlet condition with random particle injection
   - **Outflow** (bottom): Dirichlet condition (absorbing)
   - **Walls** (left/right): Slip (reflective) conditions

## Project Structure

├── proj_serial.c      # Serial implementation
├── proj_parallel.c    # MPI parallel implementation
├── proj_parallel.sh   # SLURM batch submission script
├── README.md          # This file
└── .gitignore         # Git ignore rules


## Building

### Prerequisites

| Component | Required For |
|-----------|-------------|
| C compiler (gcc, icc, clang) | Both versions |
| MPI library (OpenMPI, MPICH, Intel MPI) | Parallel version only |
| SLURM workload manager | Cluster job submission |

### Serial Version
```bash
gcc -o proj_serial proj_serial.c -lm
