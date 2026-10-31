# City Road Network Shortest Path Finder

A menu-driven C++ console application that models a city's road network as a **weighted, undirected graph** and finds the shortest route between two locations using **Dijkstra's Algorithm**.

> **Course:** CCE III – Course Project (Unit V: Trees and Graphs)

---

## 1. Problem Statement

Finding the quickest way to travel between two places is an everyday problem for navigation apps, delivery services and emergency vehicles. A city's junctions and roads naturally form a graph, so this project lets the user build a small road network and automatically computes the shortest route and its total distance.

## 2. Objectives

- Apply graph concepts to solve a real-world routing problem.
- Implement a graph using an adjacency matrix in C++.
- Implement Dijkstra's shortest path algorithm and reconstruct the actual path.
- Implement BFS and DFS traversals to explore the road network.
- Provide a simple, user-friendly menu interface with input validation.

## 3. Why a Graph? (Data Structure Justification)

| Real-world element | Graph element |
|---|---|
| Location / junction | Vertex |
| Road between locations | Edge |
| Road length (km) | Edge weight |
| Two-way roads | Undirected edge |

- A graph is the natural fit because locations can connect in arbitrary ways (not hierarchical, so a tree is not enough).
- An **adjacency matrix** (`int adjMatrix[20][20]`) gives O(1) edge lookup and is simple to implement for a small network.
- City names are stored in a parallel array (`cityNames[]`) indexed by vertex ID.

## 4. Features

1. Add a location (vertex)
2. Add a road with distance (bidirectional edge)
3. Display all locations and the adjacency matrix
4. Find the shortest path and total distance (Dijkstra)
5. BFS traversal from a chosen location
6. DFS traversal from a chosen location
7. Exit

Error handling covers: invalid location IDs, exceeding maximum capacity (20 locations), and unreachable destinations.

## 5. Algorithms

### 5.1 Dijkstra's Shortest Path

1. Set the distance of the source to 0 and all others to infinity.
2. Repeatedly pick the unvisited vertex with the smallest distance.
3. Mark it visited and relax the distances of its neighbours.
4. Store each vertex's `parent` so the path can be rebuilt.
5. Print the path recursively from the destination back to the source.

**Time complexity:** O(V²) with the adjacency matrix  
**Space complexity:** O(V²) for the matrix, O(V) for the helper arrays

### 5.2 Breadth-First Search (BFS)

Starts at a chosen location and visits all directly connected locations first, then the next level, using an array-based **queue**. Useful for finding the fewest number of road hops. Time: O(V²).

### 5.3 Depth-First Search (DFS)

Starts at a chosen location and goes as deep as possible along one road before backtracking, using **recursion** (the call stack). Useful for checking connectivity and exploring the network. Time: O(V²).

## 6. Project Structure

```
.
├── main.cpp      # Graph class + menu-driven program
└── README.md
```

## 7. How to Compile and Run

**Requirements:** a C++ compiler such as g++ (C++11 or later).

```bash
g++ main.cpp -o route_finder
./route_finder          # Linux / macOS
route_finder.exe        # Windows
```

## 8. Usage

Follow the on-screen menu:

1. Add locations first (they are assigned IDs 0, 1, 2, ...).
2. Add roads using the location IDs and a distance in km.
3. Choose option 4 for the shortest path (source and destination IDs).
4. Choose option 5 or 6 for a BFS or DFS traversal from a starting ID.

> Note: location names are read with `cin >>`, so use single words (e.g. `City_Center` instead of `City Center`).

## 9. Test Case and Sample Output

**Input network:**

| Road | Distance |
|---|---|
| College (0) – Station (1) | 4 km |
| Station (1) – Market (2) | 3 km |
| College (0) – Market (2) | 10 km |

**Query:** shortest path from College (0) to Market (2)

```
========================================
       SHORTEST ROUTE FINDER RESULTS
========================================
Source      : College
Destination : Market
Total Distance: 7 km
Optimal Path: College -> Station -> Market
========================================
```

The direct road is 10 km, but Dijkstra correctly finds the shorter 7 km route through Station.

| Test | Expected Result | Status |
|---|---|---|
| College → Market | 7 km via Station | Pass |
| Invalid location ID | Error message shown | Pass |
| Disconnected locations | "No path exists" message | Pass |
| BFS from College (0) | College -> Station -> Market -> Hostel | Pass |
| DFS from College (0) | College -> Station -> Market -> Hostel | Pass |

## 10. AI Assistance Disclosure

AI tools were used for guidance and code suggestions. I reviewed, tested and understood the code, including the Dijkstra logic, the `parent[]` array used for path reconstruction, and the menu flow. *(Edit this section to list what you personally modified or debugged.)*

## 11. Future Improvements

- Use an adjacency list with a priority queue for O(E log V) performance.
- Add connectivity checks and a minimum spanning tree (Prim's/Kruskal's).
- Support names with spaces and loading maps from a file.

## 12. Author

**Mansi Kanawade** – Roll No. 6014  
GitHub: [kanawademansi](https://github.com/kanawademansi)
