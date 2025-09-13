Of course\! Here is a `README.md` file that explains your Level 1 Vehicle Routing Problem project.

-----

# Vehicle Routing Problem (VRP) Solver using a Genetic Algorithm - Level 1

This project provides a foundational implementation of a Genetic Algorithm (GA) to solve the Capacitated Vehicle Routing Problem (CVRP). The goal is to find the most efficient set of routes for a fleet of vehicles to serve a group of customers, minimizing the total distance traveled while respecting the capacity constraints of each vehicle.

## 📝 Table of Contents

  - [Problem Description](https://www.google.com/search?q=%23-problem-description)
  - [Algorithm: Genetic Algorithm (GA)](https://www.google.com/search?q=%23-algorithm-genetic-algorithm-ga)
  - [Features](https://www.google.com/search?q=%23-features)
  - [How to Run](https://www.google.com/search?q=%23-how-to-run)
  - [Code Structure](https://www.google.com/search?q=%23-code-structure)

-----

## 🎯 Problem Description

The Vehicle Routing Problem is a classic combinatorial optimization challenge. This implementation addresses the following scenario:

  * A **single central depot** acts as the starting and ending point for all vehicles.
  * A set of **customers**, each with a specific demand for goods, are located at various coordinates.
  * A **fleet of vehicles**, each with a limited carrying **capacity**.

The objective is to find a set of routes that:

1.  Serves every customer exactly once.
2.  Ensures the total demand on any single route does not exceed the vehicle's capacity.
3.  **Minimizes the total distance** traveled by all vehicles combined.

-----

## 🧬 Algorithm: Genetic Algorithm (GA)

A Genetic Algorithm is used to explore the vast search space of possible routes and converge on a near-optimal solution. It mimics the process of natural selection.

### Key Components of the GA

#### 1\. Chromosome Representation

A unique approach is used to represent a complete solution (all routes) in a single list, called a **chromosome**. The chromosome is a permutation of all customer IDs and a set of special numbers called **"separators"**.

  * There are `(number_of_vehicles - 1)` separators.
  * These separators act as dividers, splitting the list of customers into distinct routes.

For example, with 20 customers (IDs 1-20) and 4 vehicles, we use 3 separators (e.g., 21, 22, 23). A chromosome might look like this:
`[5, 12, 8, **21**, 19, 2, 1, **22**, 15, 4, 7, 3, **23**, 6, ...]`

This translates to:

  - **Vehicle 1 Route:** Depot → 5 → 12 → 8 → Depot
  - **Vehicle 2 Route:** Depot → 19 → 2 → 1 → Depot
  - **Vehicle 3 Route:** Depot → 15 → 4 → 7 → 3 → Depot
  - **Vehicle 4 Route:** Depot → 6 → ... → Depot

#### 2\. Fitness Function

The "fitness" of a solution determines how good it is. Since our goal is to **minimize distance**, a lower fitness score is better.

  - **Total Distance:** The sum of the Euclidean distances of all routes.
  - **Penalty for Overload:** If a route's total demand exceeds the vehicle's capacity, a large penalty is added to the fitness score. This heavily discourages invalid solutions from surviving into the next generation.
    $Fitness = TotalDistance + (TotalOverload \\times PenaltyFactor)$

#### 3\. Selection

**Tournament Selection** is used to choose parent chromosomes for breeding. A small, random subset of the population (a "tournament") is selected, and the individual with the best (lowest) fitness in that group is chosen as a parent.

#### 4\. Crossover

**Edge Recombination Crossover (ERX)** is employed. ERX is highly effective for permutation-based problems like VRP because it preserves adjacency information (which customers are next to each other) from both parents, helping create high-quality offspring.

#### 5\. Mutation

**Reinsert Mutation** is used to introduce genetic diversity. It works by:

1.  Randomly selecting a customer from the chromosome.
2.  Removing it from its current position.
3.  Re-inserting it at a new random position.

#### 6\. Elitism

The best solutions from the current generation are automatically carried over to the next generation. This ensures that the algorithm's progress is never lost.

-----

## ✨ Features

  * Solves the Capacitated Vehicle Routing Problem (CVRP).
  * Implements a robust Genetic Algorithm with advanced operators (Tournament Selection, ERX).
  * Includes a penalty function to handle vehicle capacity constraints effectively.
  * Automatically generates a random problem instance (customers, demands) for easy demonstration.
  * Visualizes the final best solution, showing all vehicle routes clearly.
  * Plots the fitness history, showing how the solution quality improves over generations.

-----

## 🚀 How to Run

### Prerequisites

You need Python 3 and the `matplotlib` library.

```bash
pip install matplotlib
```

### Execution

1.  Save the code as `vrp_Level_01.py`.
2.  Run the script from your terminal:
    ```bash
    python vrp_Level_01.py
    ```
3.  The script will print the progress of the genetic algorithm in the console. Once finished, it will display the final routes and a plot window will appear showing the solution map and fitness graph.

-----

## 📂 Code Structure

  * `VRPProblem` **Class**: A data container that holds all the information about the VRP instance, including locations, demands, vehicle count, and a pre-computed distance matrix for efficiency.
  * `GeneticAlgorithm` **Class**: The core of the solver. It contains all the logic for the GA, including population initialization, fitness calculation, selection, crossover, and mutation.
  * `plot_solution_and_history()` **Function**: A utility function that uses `matplotlib` to create the final visualizations.
  * `if __name__ == "__main__":` **Block**: The main execution block where the problem is defined, the GA is configured and run, and the final results are printed and plotted.