# Multi Path Solver

## Description

**Multi Path Solver** is a multi-agent pathfinding solution developed in C. The program efficiently routes multiple entities through a network from a source node to a destination node, minimizing total traversal time while respecting capacity constraints.

This project implements advanced graph algorithms to find optimal path combinations and manage concurrent entity movement through a network of interconnected nodes.

## Objective

The goal is to route all entities from the source (`##start`) to the sink (`##end`) in minimum time, with constraints:
- Each intermediate node can hold at most one entity at a time
- Entities move along edges between nodes
- Each entity moves exactly one step per time unit
- Multiple paths must be utilized efficiently to minimize congestion

## Project Structure

```
.
├── include/          # Header files (.h)
├── lib/             # External libraries
├── src/             # Source code (.c)
├── tests/           # Test files and graph examples
├── Makefile         # Compilation file
└── gen_map.pl       # Graph generator (Perl)
```

## Compilation

To compile the project, simply use the command:

```bash
make
```

This generates the executable.

To clean object files:

```bash
make clean
```

To clean completely (objects + executable):

```bash
make fclean
```

To recompile entirely:

```bash
make re
```

## Usage

The program reads a graph description from standard input:

```bash
./amazed < tests/graph_example.txt
```

### Input Format

The graph must follow this format:

```
[number_of_entities]
##start
[source_node] [x] [y]
##end
[sink_node] [x] [y]
[node_name] [x] [y]
...
[node1]-[node2]
[node2]-[node3]
...
```

**Graph Example:**

```
4
##start
start 0 0
##end
end 6 0
node1 2 0
node2 4 0
start-node1
node1-node2
node2-end
start-end
```

### Output Format

The program displays:
1. The input graph (number of entities, nodes, edges)
2. Entity movements at each time step

Movement format: `L[entity_id]-[node_name]`

**Output Example:**

```
4
##start
start 0 0
##end
end 6 0
node1 2 0
node2 4 0
start-node1
node1-node2
node2-end
start-end

L1-end L2-end L3-end L4-end
```

## Pathfinding Algorithms

The project implements various graph algorithms:

- **Dijkstra's Algorithm**: Finds shortest paths in weighted graphs
- **Breadth-First Search (BFS)**: Level-by-level graph exploration for unweighted graphs
- **Edmonds-Karp**: Maximum flow algorithm using augmenting paths
- **Ford-Fulkerson**: Computes maximum flow in flow networks
- **Disjoint Path Finding**: Identifies multiple non-overlapping paths

## Optimization Strategy

The program implements a multi-phase approach:

1. **Graph Construction**: Parse input and build adjacency list representation
2. **Path Discovery**: Find all simple paths from source to sink
3. **Flow Analysis**: Compute maximum flow and identify bottlenecks
4. **Path Selection**: Choose optimal path combination based on entity count
5. **Entity Distribution**: Assign entities to paths to minimize makespan
6. **Simulation**: Execute movements with conflict resolution

### Key Optimizations

- **Multi-path routing**: Utilize parallel paths to reduce completion time
- **Load balancing**: Distribute entities across paths optimally
- **Greedy scheduling**: Minimize idle time for each entity
- **Conflict avoidance**: Prevent node and edge collisions

## Technical Constraints

### Implementation Requirements
- Language: C
- No memory leaks
- Robust error handling (no segfault, bus error, etc.)
- Limited to: `write`, `read`, `malloc`, `free`, `exit`

### Graph Constraints
- Entities move one edge per time step
- Each edge supports one entity per time step
- Intermediate nodes have capacity of 1 (source and sink are unlimited)
- All entities start at the source node
- Goal: minimize total time to reach sink

## Testing

The `tests/` folder contains graphs of varying complexity:
- **Simple**: Single path or minimal branching
- **Medium**: Multiple disjoint paths
- **Complex**: Dense graphs with many alternatives

Generate custom test graphs:

```bash
perl gen_map.pl --flow-one --big > test_graph.txt
./lem_in < test_graph.txt
```

## Core Concepts

This project explores fundamental computer science topics:

- **Graph Theory**: Representation (adjacency lists/matrices), traversal algorithms
- **Pathfinding**: Single-source shortest paths, all-pairs shortest paths
- **Network Flow**: Maximum flow, minimum cut, flow decomposition
- **Optimization**: Makespan minimization, load balancing
- **Data Structures**: Linked lists, queues, hash tables, priority queues
- **Algorithm Complexity**: Time/space analysis, optimization techniques
- **Memory Management**: Dynamic allocation, garbage prevention

## Author
**Rayan**

GitHub: @Rayan-ouer


---
