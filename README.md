# Ant Colony Optimization (ACO) on a Metabolic Graph

This repository implements the **Ant Colony Optimization (ACO)** algorithm to find the **minimum-cost path** between two nodes in a **metabolic graph**, using a distance matrix stored in a `.npz` file.

---
  
  ##
  
  This project demonstrates the application of **ACO** to a weighted graph representing a metabolic network.  
The algorithm is inspired by the foraging behavior of ants, which deposit pheromones to communicate and collectively find optimal paths.

It loads a `.npz` dataset containing a distance matrix and node coordinates, constructs a graph using **NetworkX**, and then iteratively improves paths between two nodes until it finds the optimal route.

---
  
  ##Project Steps
  
  1. **Load Data**  
  - Reads `Dist` (distance matrix) and `coords` (node coordinates) from a `.npz` file.  
- The file `metabolic_graph.npz` must be located in `/content/`.

2. **Create the Graph**  
  - Builds a **NetworkX** weighted graph from the distance matrix.  
- Assigns coordinates as node attributes for visualization.

3. **Initialize Parameters**  
  - Defines the ACO hyperparameters and pheromone trails.

4. **Run the Algorithm**  
  - Each ant constructs a possible path between `start_node` and `end_node`.  
- Pheromone levels are updated iteratively based on the quality of discovered paths.

5. **Visualization**  
  - Displays the graph and highlights the best path found by ACO.

---
  
  ##Requirements
  
  Install dependencies before running the script:
  
  ```bash
pip install numpy networkx matplotlib
```

---
  
  ##  Expected `.npz` File Structure
  
  The `.npz` file must contain the following arrays:
  
  | Key | Description |
  |-----|--------------|
  | `Dist` | NxN distance matrix between nodes. |
  | `coords` | Nx2 matrix with x and y coordinates of each node. |
  
  Example to create a compatible `.npz` file:
  
  ```python
import numpy as np

Dist = np.random.rand(20, 20)
Dist = (Dist + Dist.T) / 2  # Symmetrize
np.fill_diagonal(Dist, 0)
coords = np.random.rand(20, 2)

np.savez('metabolic_graph.npz', Dist=Dist, coords=coords)
```

---
  
  ##  ACO Parameters Used
  
  These are the **exact parameters** used in this implementation:
  
  | Parameter | Symbol | Value | Description |
  |------------|---------|--------|--------------|
  | Number of ants | `num_ants` | **20** | Number of ants per iteration |
  | Number of iterations | `num_iterations` | **100** | Total iterations of the algorithm |
  | Pheromone influence | `alpha` | **1.0** | Weight of pheromone importance |
  | Heuristic influence | `beta` | **2.0** | Weight of heuristic importance (1/distance) |
  | Evaporation rate | `rho` | **0.5** | Fraction of pheromone evaporated each iteration |
  | Pheromone deposit factor | `q` | **100.0** | Pheromone deposited per path |
  | Initial pheromone level | `initial_pheromone` | **0.1** | Starting pheromone value on all edges |
  | Start node | `start_node` | **0** | Starting node index |
  | End node | `end_node` | **19** | Destination node index |
  
  ---
  
  
  
  ##  Execution
  
  1. Place the file `metabolic_graph.npz` in the correct path (`/content/` or adjust it in the script).
2. Run the main script:
  
  ```bash
python main.py
```

3. The program will:
  - Load and inspect the `.npz` data.
- Create the metabolic graph.
- Run the ACO algorithm for 100 iterations.
- Display progress and best results in the console.
- Show a graphical representation of the optimal path.

---
  
  ## Output Information
  
  ### Console Output
  - Details of the `.npz` file contents.  
- Graph information (nodes, edges, attributes).  
- Progress logs for each iteration (every 10 steps).  
- The best path found and its total cost.

Example:
  ```
Iteration 100/100: Current best path cost = 42.37
Best path found: [0, 5, 7, 10, 13, 19]
Minimum cost of best path: 42.37
```

---
  
  ## Graphical Output
  
  The algorithm produces a **Matplotlib plot** showing:
  -  **Gray**: Other nodes and edges.  
-  **Red**: Start and end nodes.  
-  **Blue**: Intermediate nodes in the best path.  
-  **Red edges**: Edges belonging to the best path.

The plot includes a title, legend, and node labels.

---
  
  ##  Concepts Behind ACO
  
  - **Pheromone trail**: A simulated chemical trace used to guide ants toward favorable paths.
- **Heuristic**: Inverse of the distance (shorter paths are more attractive).
- **Exploration vs. Exploitation**: Controlled by `alpha` (pheromone weight) and `beta` (heuristic weight).
- **Evaporation**: Avoids stagnation by reducing pheromone concentration over time.

---
  
  
  
  ---
  
  ##  Author
  
  **Developed by:** [VALENTINA PORRAS] 
**Language:** Python 3  
**Libraries:** NumPy, NetworkX, Matplotlib  

---
  
  ## Acknowledgments
  
  This implementation is based on the classical **Ant Colony Optimization (ACO)** metaheuristic, widely applied in pathfinding, logistics, and biological network optimization.  
It serves as an educational and research tool for exploring **bioinformatics**, **complex systems**, and **evolutionary computation**.

---

  
