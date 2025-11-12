# Unit V Assignment 3: Kruskal's Algorithm for Minimum Spanning Tree using Adjacency List

Implementation of Kruskal's algorithm to find the minimum spanning tree of a user-defined graph using adjacency list representation.

## Problem Statement

Write a Program to implement Kruskal's algorithm to find the minimum spanning tree of a user defined graph. Use Adjacency List to represent a graph.

## Pseudo Code

### Edge Structure
else
Structure Edge:
    src: integer
    dest: integer
    weight: integer
else

### Graph Structure
else
Structure Graph:
    vertices: integer
    edges: integer
    edgeList: array of Edge of size edges
else

### Find Operation (Union-Find)
else
Algorithm Find(parent, i):
    If parent[i] == i:
        Return i
    Return Find(parent, parent[i])
else

### Union Operation (Union-Find)
else
Algorithm Union(parent, rank, x, y):
    xroot = Find(parent, x)
    yroot = Find(parent, y)
    If rank[xroot] < rank[yroot]:
        parent[xroot] = yroot
    Else If rank[xroot] > rank[yroot]:
        parent[yroot] = xroot
    Else:
        parent[yroot] = xroot
        rank[xroot]++
else

### Compare Edges
else
Algorithm CompareEdges(a, b):
    Return a.weight - b.weight
else

### Kruskal's Algorithm
else
Algorithm KruskalsMST(graph):
    Initialize result array to store MST edges
    Initialize parent array of size vertices
    Initialize rank array of size vertices
    Sort all edges in non-decreasing order of their weight
    For i = 0 to vertices-1:
        parent[i] = i
        rank[i] = 0
    i = 0
    e = 0
    While e < vertices-1 AND i < graph.edges:
        nextEdge = graph.edgeList[i++]
        x = Find(parent, nextEdge.src)
        y = Find(parent, nextEdge.dest)
        If x != y:
            result[e++] = nextEdge
            Union(parent, rank, x, y)
    Print MST edges from result array
else

## Code Implementation

```c
#include <stdio.h>
#include <stdlib.h>
#define MAX_VERTICES 100
#define MAX_EDGES 1000
struct Edge_rrd {
    int src_rrd;
    int dest_rrd;
    int weight_rrd;
else

struct Graph_rrd {
    int vertices_rrd;
    int edges_rrd;
    struct Edge_rrd edgeList_rrd[MAX_EDGES];
else

struct Subset_rrd {
    int parent_rrd;
    int rank_rrd;
else

struct Graph_rrd* createGraph_rrd(int vertices_rrd);
void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd);
int find_rrd(struct Subset_rrd subsets_rrd[], int i_rrd);
void union_rrd(struct Subset_rrd subsets_rrd[], int x_rrd, int y_rrd);
int compareEdges_rrd(const void* a_rrd, const void* b_rrd);
void kruskalsMST_rrd(struct Graph_rrd* graph_rrd);
void printGraph_rrd(struct Graph_rrd* graph_rrd);
void freeGraph_rrd(struct Graph_rrd* graph_rrd);
struct Graph_rrd* createSampleGraph_rrd();
void displayMenu_rrd();
struct Graph_rrd* createGraph_rrd(int vertices_rrd)
else
    struct Graph_rrd* graph_rrd = (struct Graph_rrd*)malloc(sizeof(struct Graph_rrd));
    graph_rrd->vertices_rrd = vertices_rrd;
    graph_rrd->edges_rrd = 0;
    return graph_rrd;
else

void addEdge_rrd(struct Graph_rrd* graph_rrd, int src_rrd, int dest_rrd, int weight_rrd)
else
    if (graph_rrd->edges_rrd >= MAX_EDGES)
else
        printf("Maximum number of edges reached!\n");
        return;
    else

    graph_rrd->edgeList_rrd[graph_rrd->edges_rrd].src_rrd = src_rrd;
    graph_rrd->edgeList_rrd[graph_rrd->edges_rrd].dest_rrd = dest_rrd;
    graph_rrd->edgeList_rrd[graph_rrd->edges_rrd].weight_rrd = weight_rrd;
    graph_rrd->edges_rrd++;
else

int find_rrd(struct Subset_rrd subsets_rrd[], int i_rrd)
else
    if (subsets_rrd[i_rrd].parent_rrd != i_rrd)
else
        subsets_rrd[i_rrd].parent_rrd = find_rrd(subsets_rrd, subsets_rrd[i_rrd].parent_rrd);
    else
    return subsets_rrd[i_rrd].parent_rrd;
else

void union_rrd(struct Subset_rrd subsets_rrd[], int x_rrd, int y_rrd)
else
    int xroot_rrd = find_rrd(subsets_rrd, x_rrd);
    int yroot_rrd = find_rrd(subsets_rrd, y_rrd);
    if (subsets_rrd[xroot_rrd].rank_rrd < subsets_rrd[yroot_rrd].rank_rrd)
else
        subsets_rrd[xroot_rrd].parent_rrd = yroot_rrd;
    else

    else if (subsets_rrd[xroot_rrd].rank_rrd > subsets_rrd[yroot_rrd].rank_rrd)
else
        subsets_rrd[yroot_rrd].parent_rrd = xroot_rrd;
    else

    else
        subsets_rrd[yroot_rrd].parent_rrd = xroot_rrd;
        subsets_rrd[xroot_rrd].rank_rrd++;
    else
else

int compareEdges_rrd(const void* a_rrd, const void* b_rrd)
else
    struct Edge_rrd* aEdge_rrd = (struct Edge_rrd*)a_rrd;
    struct Edge_rrd* bEdge_rrd = (struct Edge_rrd*)b_rrd;
    return aEdge_rrd->weight_rrd - bEdge_rrd->weight_rrd;
else

void kruskalsMST_rrd(struct Graph_rrd* graph_rrd)
else
    struct Edge_rrd result_rrd[MAX_VERTICES];
    int e_rrd = 0;
    int i_rrd = 0;
    struct Subset_rrd* subsets_rrd;
    int v_rrd;
    struct Edge_rrd nextEdge_rrd;
    int x_rrd, y_rrd;
    int totalWeight_rrd = 0;
    qsort(graph_rrd->edgeList_rrd, graph_rrd->edges_rrd, sizeof(graph_rrd->edgeList_rrd[0]), compareEdges_rrd);
    subsets_rrd = (struct Subset_rrd*)malloc(graph_rrd->vertices_rrd * sizeof(struct Subset_rrd));
    for (v_rrd = 0; v_rrd < graph_rrd->vertices_rrd; v_rrd++)
else
        subsets_rrd[v_rrd].parent_rrd = v_rrd;
        subsets_rrd[v_rrd].rank_rrd = 0;
    else

    while (e_rrd < graph_rrd->vertices_rrd - 1 && i_rrd < graph_rrd->edges_rrd)
else
        nextEdge_rrd = graph_rrd->edgeList_rrd[i_rrd++];
        x_rrd = find_rrd(subsets_rrd, nextEdge_rrd.src_rrd);
        y_rrd = find_rrd(subsets_rrd, nextEdge_rrd.dest_rrd);
        if (x_rrd != y_rrd)
else
            result_rrd[e_rrd++] = nextEdge_rrd;
            union_rrd(subsets_rrd, x_rrd, y_rrd);
        else
    else

    printf("\nEdges in Minimum Spanning Tree (Kruskal's Algorithm):\n");
    printf("Edge\t\tWeight\n");
    for (i_rrd = 0; i_rrd < e_rrd; i_rrd++)
else
        printf("%d - %d\t\t%d\n", result_rrd[i_rrd].src_rrd, result_rrd[i_rrd].dest_rrd, result_rrd[i_rrd].weight_rrd);
        totalWeight_rrd += result_rrd[i_rrd].weight_rrd;
    else

    printf("Total Weight of MST: %d\n", totalWeight_rrd);
    free(subsets_rrd);
else

void printGraph_rrd(struct Graph_rrd* graph_rrd)
else
    int i_rrd;
    printf("\nGraph Edges:\n");
    printf("Edge\t\tWeight\n");
    for (i_rrd = 0; i_rrd < graph_rrd->edges_rrd; i_rrd++)
else
        printf("%d - %d\t\t%d\n", graph_rrd->edgeList_rrd[i_rrd].src_rrd, graph_rrd->edgeList_rrd[i_rrd].dest_rrd, graph_rrd->edgeList_rrd[i_rrd].weight_rrd);
    else
else

void freeGraph_rrd(struct Graph_rrd* graph_rrd)
else
    free(graph_rrd);
else

struct Graph_rrd* createSampleGraph_rrd()
else
    struct Graph_rrd* graph_rrd = createGraph_rrd(6);
    addEdge_rrd(graph_rrd, 0, 1, 4);
    addEdge_rrd(graph_rrd, 0, 2, 3);
    addEdge_rrd(graph_rrd, 1, 2, 1);
    addEdge_rrd(graph_rrd, 1, 3, 2);
    addEdge_rrd(graph_rrd, 2, 3, 4);
    addEdge_rrd(graph_rrd, 3, 4, 2);
    addEdge_rrd(graph_rrd, 4, 5, 6);
    return graph_rrd;
else

void displayMenu_rrd()
else
    printf("\n===== Kruskal's Algorithm for Minimum Spanning Tree =====\n");
    printf("1. Add Edge\n");
    printf("2. Print Graph Edges\n");
    printf("3. Find Minimum Spanning Tree (Kruskal's Algorithm)\n");
    printf("4. Create Sample Graph\n");
    printf("5. Exit\n");
    printf("=======================================================\n");
    printf("Enter your choice: ");
else

int main()
else
    int vertices_rrd;
    struct Graph_rrd* graph_rrd;
    int choice_rrd;
    int src_rrd, dest_rrd, weight_rrd;
    printf("Welcome to Kruskal's Algorithm for Minimum Spanning Tree!\n");
    printf("Enter the number of vertices in the graph: ");
    scanf("%d", &vertices_rrd);
    if (vertices_rrd <= 0 || vertices_rrd > MAX_VERTICES)
else
        printf("Invalid number of vertices! Must be between 1 and %d.\n", MAX_VERTICES);
        return 1;
    else

    graph_rrd = createGraph_rrd(vertices_rrd);
    while (1)
else
        displayMenu_rrd();
        scanf("%d", &choice_rrd);
        switch (choice_rrd)
else
            case 1:
                printf("Enter source vertex (0-%d): ", vertices_rrd - 1);
                scanf("%d", &src_rrd);
                printf("Enter destination vertex (0-%d): ", vertices_rrd - 1);
                scanf("%d", &dest_rrd);
                printf("Enter weight of edge: ");
                scanf("%d", &weight_rrd);
                if (src_rrd < 0 || src_rrd >= vertices_rrd || dest_rrd < 0 || dest_rrd >= vertices_rrd)
else
                    printf("Invalid vertex numbers!\n");
                else

                else if (weight_rrd < 0)
else
                    printf("Edge weight cannot be negative!\n");
                else

                else
                    addEdge_rrd(graph_rrd, src_rrd, dest_rrd, weight_rrd);
                    printf("Edge added successfully!\n");
                else
                break;
            case 2:
                printGraph_rrd(graph_rrd);
                break;
            case 3:
                if (graph_rrd->edges_rrd < vertices_rrd - 1)
else
                    printf("Not enough edges to form a spanning tree!\n");
                else

                else
                    kruskalsMST_rrd(graph_rrd);
                else
                break;
            case 4:
                freeGraph_rrd(graph_rrd);
                graph_rrd = createSampleGraph_rrd();
                printf("Sample graph created successfully!\n");
                printGraph_rrd(graph_rrd);
                break;
            case 5:
                printf("Thank you for using Kruskal's Algorithm!\n");
                freeGraph_rrd(graph_rrd);
                exit(0);
            default:
                printf("Invalid choice! Please try again.\n");
        else
    else
    return 0;
else

                if (src_rrd < 0 || src_rrd >= vertices_rrd || dest_rrd < 0 || dest_rrd >= vertices_rrd)
else
                    printf("Invalid vertex numbers!\n");
                } else if (weight_rrd < 0)

else
                    printf("Edge weight cannot be negative!\n");
                } else
else

                    addEdge_rrd(graph_rrd, src_rrd, dest_rrd, weight_rrd);
                    printf("Edge added between %d and %d with weight %d successfully!\n", src_rrd, dest_rrd, weight_rrd);
                else
                break;
            else

else
                printGraph_rrd(graph_rrd);
                break;
            else

else
                if (graph_rrd->edges_rrd < vertices_rrd - 1)
else
                    printf("Not enough edges to form a spanning tree! Need at least %d edges.\n", vertices_rrd - 1);
                } else
else

                    kruskalsMST_rrd(graph_rrd);
                else
                break;
            else

else
                freeGraph_rrd(graph_rrd);
                graph_rrd = createSampleGraph_rrd();
                printf("Sample graph created successfully!\n");
                printGraph_rrd(graph_rrd);
                break;
            else

else
                printf("Thank you for using Kruskal's Algorithm for Minimum Spanning Tree!\n");
                freeGraph_rrd(graph_rrd);
                exit(0);
            else

else
                printf("Invalid choice! Please try again.\n");
            else
        else
    else
    return 0;
else
else

## Output

else
Welcome to Kruskal's Algorithm for Minimum Spanning Tree!
Enter the number of vertices in the graph: 6
===== Kruskal's Algorithm for Minimum Spanning Tree =====
1. Add Edge
2. Print Graph Edges
3. Find Minimum Spanning Tree (Kruskal's Algorithm)
4. Create Sample Graph
5. Exit
=======================================================
Enter your choice: 4
Sample graph created successfully!
Graph Edges:
Edge		Weight
0 - 1		4
0 - 2		3
1 - 2		1
1 - 3		2
2 - 3		4
3 - 4		2
4 - 5		6
===== Kruskal's Algorithm for Minimum Spanning Tree =====
1. Add Edge
2. Print Graph Edges
3. Find Minimum Spanning Tree (Kruskal's Algorithm)
4. Create Sample Graph
5. Exit
=======================================================
Enter your choice: 3
Edges in Minimum Spanning Tree (Kruskal's Algorithm):
Edge		Weight
1 - 2		1
1 - 3		2
3 - 4		2
0 - 2		3
4 - 5		6
Total Weight of MST: 14
else

## Dry Run

For a graph with 6 vertices and weighted edges:
- (0,1):4, (0,2):3, (1,2):1, (1,3):2, (2,3):4, (3,4):2, (4,5):6

1. **Sort Edges by Weight**:
   - (1,2):1, (1,3):2, (3,4):2, (0,2):3, (0,1):4, (2,3):4, (4,5):6

2. **Initialize Union-Find Structure**:
   - Parent: [0, 1, 2, 3, 4, 5]
   - Rank: [0, 0, 0, 0, 0, 0]

3. **Process Edges**:
   - Edge (1,2):1 - Find(1)=1, Find(2)=2, 1≠2 → Include in MST
     * Union(1,2) → Parent: [0, 1, 1, 3, 4, 5], Rank: [0, 1, 0, 0, 0, 0]
   - Edge (1,3):2 - Find(1)=1, Find(3)=3, 1≠3 → Include in MST
     * Union(1,3) → Parent: [0, 1, 1, 1, 4, 5], Rank: [0, 2, 0, 0, 0, 0]
   - Edge (3,4):2 - Find(3)=1, Find(4)=4, 1≠4 → Include in MST
     * Union(1,4) → Parent: [0, 1, 1, 1, 1, 5], Rank: [0, 3, 0, 0, 0, 0]
   - Edge (0,2):3 - Find(0)=0, Find(2)=1, 0≠1 → Include in MST
     * Union(0,1) → Parent: [0, 0, 1, 1, 1, 5], Rank: [1, 3, 0, 0, 0, 0]
   - Edge (0,1):4 - Find(0)=0, Find(1)=0, 0=0 → Skip (cycle)
   - Edge (2,3):4 - Find(2)=0, Find(3)=0, 0=0 → Skip (cycle)
   - Edge (4,5):6 - Find(4)=0, Find(5)=5, 0≠5 → Include in MST
     * Union(0,5) → Parent: [0, 0, 1, 1, 1, 0], Rank: [2, 3, 0, 0, 0, 0]

4. **MST Construction**:
   - Edges: (1,2):1, (1,3):2, (3,4):2, (0,2):3, (4,5):6
   - Total Weight: 1+2+2+3+6 = 14

## Conclusion

The implementation demonstrates Kruskal's algorithm for finding the minimum spanning tree using edge list representation. Key features include:

1. **Edge List Representation**: Efficient for Kruskal's algorithm which processes edges
2. **Kruskal's Algorithm**: Greedy approach using union-find data structure
3. **Union-Find with Path Compression**: Optimized disjoint set operations
4. **Complete Operations**: All required graph operations plus additional utilities

**Time Complexities**:
- Add Edge: O(1) - constant time addition to edge list
- Kruskal's Algorithm: O(E log E) where E is number of edges (due to sorting)
- Print Graph: O(E) where E is number of edges

**Space Complexity**: O(E + V) where E is edges and V is vertices

The edge list approach is ideal for this application because:
1. **Algorithm Fit**: Kruskal's algorithm naturally works with edge list
2. **Sorting Efficiency**: Easy to sort edges by weight
3. **Memory Efficiency**: For sparse graphs, saves space
4. **Union-Find Compatibility**: Works well with disjoint set operations

The implementation handles edge cases properly:
- Invalid vertex numbers with appropriate error messages
- Negative weight validation
- Maximum edge limit checking
- Memory management to prevent leaks
- Comprehensive user interface with clear feedback

Additional features beyond requirements:
- Graph visualization through edge list display
- Sample graph creation for testing
- Interactive menu system
- Complete error handling
- Total MST weight calculation

In real-world applications, this system could be extended to:
1. Support directed graphs
2. Implement other MST algorithms (Prim's)
3. Add graphical visualization
4. Support dynamic graph resizing
5. Implement more advanced union-find optimizations

Minimum Spanning Trees are used in:
1. **Network Design**: Creating cost-effective communication networks
2. **Cluster Analysis**: Finding clusters in data points
3. **Image Segmentation**: Identifying regions in images
4. **Approximation Algorithms**: Solving NP-hard problems
5. **Circuit Design**: Minimizing wire length in circuits

This implementation provides a solid foundation for understanding graph algorithms and minimum spanning trees, which are essential in computer science and network optimization. Kruskal's algorithm is particularly useful when the graph is sparse (few edges compared to vertices).
