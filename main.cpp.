/*
 * City Road Network Shortest Path Finder
 * CCE III - Course Project (Unit V: Trees and Graphs)
 * Author : Mansi Kanawade
 * Roll No: 6014
 *
 * Graph (adjacency matrix) with:
 *  - Dijkstra's Algorithm for shortest path
 *  - BFS and DFS traversals
 */

#include <iostream>
#include <string>

using namespace std;

const int MAX = 20;
const int INF = 99999;

class Graph {
private:
    int numVertices;
    string cityNames[MAX];
    int adjMatrix[MAX][MAX];

    // Helper: vertex with the minimum distance value not yet finalized
    int minDistance(int dist[], bool sptSet[]) {
        int min = INF, minIndex = -1;
        for (int v = 0; v < numVertices; v++) {
            if (!sptSet[v] && dist[v] <= min) {
                min = dist[v];
                minIndex = v;
            }
        }
        return minIndex;
    }

    // Helper: print the constructed path recursively
    void printPath(int parent[], int j) {
        if (parent[j] == -1) {
            cout << cityNames[j];
            return;
        }
        printPath(parent, parent[j]);
        cout << " -> " << cityNames[j];
    }

    // Helper: recursive DFS
    void dfsUtil(int u, bool visited[], bool &first) {
        visited[u] = true;
        if (!first) cout << " -> ";
        cout << cityNames[u];
        first = false;
        for (int v = 0; v < numVertices; v++) {
            if (adjMatrix[u][v] && !visited[v]) {
                dfsUtil(v, visited, first);
            }
        }
    }

public:
    Graph() {
        numVertices = 0;
        for (int i = 0; i < MAX; i++) {
            cityNames[i] = "";
            for (int j = 0; j < MAX; j++) {
                adjMatrix[i][j] = 0;
            }
        }
    }

    // Add a location/vertex
    void addVertex(string name) {
        if (numVertices >= MAX) {
            cout << "\n[Error] Maximum capacity reached! Cannot add more locations.\n";
            return;
        }
        cityNames[numVertices] = name;
        numVertices++;
        cout << "\n[Success] Location '" << name << "' added successfully with ID " << (numVertices - 1) << ".\n";
    }

    // Add a road/edge between two locations
    void addEdge(int u, int v, int weight) {
        if (u < 0 || u >= numVertices || v < 0 || v >= numVertices) {
            cout << "\n[Error] Invalid location ID(s) provided!\n";
            return;
        }
        if (u == v) {
            cout << "\n[Error] A road must connect two different locations!\n";
            return;
        }
        if (weight <= 0) {
            cout << "\n[Error] Distance must be a positive number!\n";
            return;
        }
        adjMatrix[u][v] = weight;
        adjMatrix[v][u] = weight; // bidirectional road network
        cout << "\n[Success] Road added between " << cityNames[u] << " and " << cityNames[v]
             << " with distance " << weight << " km.\n";
    }

    // Display all locations and adjacency matrix
    void displayGraph() {
        if (numVertices == 0) {
            cout << "\n[Info] Road network is currently empty.\n";
            return;
        }

        cout << "\n========================================\n";
        cout << "          CITY LOCATIONS INDEX          \n";
        cout << "========================================\n";
        for (int i = 0; i < numVertices; i++) {
            cout << "ID: " << i << " -> " << cityNames[i] << "\n";
        }

        cout << "\n========================================\n";
        cout << "      ROAD NETWORK ADJACENCY MATRIX     \n";
        cout << "========================================\n\t";
        for (int i = 0; i < numVertices; i++) {
            cout << "[" << i << "]\t";
        }
        cout << "\n";

        for (int i = 0; i < numVertices; i++) {
            cout << "[" << i << "]\t";
            for (int j = 0; j < numVertices; j++) {
                cout << adjMatrix[i][j] << "\t";
            }
            cout << "\n";
        }
        cout << "========================================\n";
    }

    // Dijkstra's Algorithm for shortest path
    void findShortestPath(int src, int dest) {
        if (src < 0 || src >= numVertices || dest < 0 || dest >= numVertices) {
            cout << "\n[Error] Invalid source or destination ID!\n";
            return;
        }

        int dist[MAX];
        bool sptSet[MAX];
        int parent[MAX];

        for (int i = 0; i < numVertices; i++) {
            dist[i] = INF;
            sptSet[i] = false;
            parent[i] = -1;
        }

        dist[src] = 0;

        for (int count = 0; count < numVertices - 1; count++) {
            int u = minDistance(dist, sptSet);
            if (u == -1) break;
            sptSet[u] = true;

            for (int v = 0; v < numVertices; v++) {
                if (!sptSet[v] && adjMatrix[u][v] && dist[u] != INF
                    && dist[u] + adjMatrix[u][v] < dist[v]) {
                    parent[v] = u;
                    dist[v] = dist[u] + adjMatrix[u][v];
                }
            }
        }

        cout << "\n========================================\n";
        cout << "       SHORTEST ROUTE FINDER RESULTS    \n";
        cout << "========================================\n";
        if (dist[dest] == INF) {
            cout << "No path exists between " << cityNames[src] << " and " << cityNames[dest] << ".\n";
        } else {
            cout << "Source      : " << cityNames[src] << "\n";
            cout << "Destination : " << cityNames[dest] << "\n";
            cout << "Total Distance: " << dist[dest] << " km\n";
            cout << "Optimal Path: ";
            printPath(parent, dest);
            cout << "\n";
        }
        cout << "========================================\n";
    }

    // Breadth-First Search (uses an array-based queue)
    void bfs(int start) {
        if (start < 0 || start >= numVertices) {
            cout << "\n[Error] Invalid starting location ID!\n";
            return;
        }

        bool visited[MAX] = {false};
        int queue[MAX];
        int front = 0, rear = 0;

        visited[start] = true;
        queue[rear++] = start;

        cout << "\n========================================\n";
        cout << "     BFS TRAVERSAL (nearest hops first)  \n";
        cout << "========================================\n";
        bool first = true;
        while (front < rear) {
            int u = queue[front++];
            if (!first) cout << " -> ";
            cout << cityNames[u];
            first = false;

            for (int v = 0; v < numVertices; v++) {
                if (adjMatrix[u][v] && !visited[v]) {
                    visited[v] = true;
                    queue[rear++] = v;
                }
            }
        }
        cout << "\n========================================\n";
    }

    // Depth-First Search (recursive)
    void dfs(int start) {
        if (start < 0 || start >= numVertices) {
            cout << "\n[Error] Invalid starting location ID!\n";
            return;
        }

        bool visited[MAX] = {false};
        bool first = true;

        cout << "\n========================================\n";
        cout << "        DFS TRAVERSAL (deepest first)    \n";
        cout << "========================================\n";
        dfsUtil(start, visited, first);
        cout << "\n========================================\n";
    }
};

int main() {
    Graph cityMap;
    int choice;

    do {
        cout << "\n*** CITY ROAD NETWORK SHORTEST PATH FINDER ***\n";
        cout << "1. Add Location (Vertex)\n";
        cout << "2. Add Road (Edge with Distance)\n";
        cout << "3. Display Road Network\n";
        cout << "4. Find Shortest Path (Dijkstra's Algorithm)\n";
        cout << "5. BFS Traversal\n";
        cout << "6. DFS Traversal\n";
        cout << "7. Exit\n";
        cout << "Enter your choice (1-7): ";

        if (!(cin >> choice)) {
            cin.clear();
            cin.ignore(10000, '\n');
            choice = 0;
        }

        switch (choice) {
            case 1: {
                string name;
                cout << "Enter location/junction name: ";
                cin >> name;
                cityMap.addVertex(name);
                break;
            }
            case 2: {
                int u, v, weight;
                cout << "Enter Source Location ID: ";
                cin >> u;
                cout << "Enter Destination Location ID: ";
                cin >> v;
                cout << "Enter Road Distance (km): ";
                cin >> weight;
                cityMap.addEdge(u, v, weight);
                break;
            }
            case 3:
                cityMap.displayGraph();
                break;
            case 4: {
                int src, dest;
                cout << "Enter Source Location ID: ";
                cin >> src;
                cout << "Enter Destination Location ID: ";
                cin >> dest;
                cityMap.findShortestPath(src, dest);
                break;
            }
            case 5: {
                int start;
                cout << "Enter Starting Location ID: ";
                cin >> start;
                cityMap.bfs(start);
                break;
            }
            case 6: {
                int start;
                cout << "Enter Starting Location ID: ";
                cin >> start;
                cityMap.dfs(start);
                break;
            }
            case 7:
                cout << "\nExiting application. Thank you!\n";
                break;
            default:
                cout << "\n[Error] Invalid choice! Please enter a number between 1 and 7.\n";
        }
    } while (choice != 7);

    return 0;
}
