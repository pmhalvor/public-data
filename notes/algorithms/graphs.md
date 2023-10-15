# Algorithms - Graphs

In this note, we cover the folling graph algorithms:
- [BFS](#bfs)
- [DFS](#dfs)
- [A*](#a)

## BFS
The breadth-first search (BFS) algorithm is a graph traversal algorithm that starts at a given node and explores all of its neighbors at the current depth before moving on to the next depth level. It is implemented using a queue data structure.

### Pseudocode
```python
def bfs(start, graph):
    visited = set()
    queue = [start]

    while queue:
        node = queue.pop(0)
        if node not in visited:
            visited.add(node)
            queue.extend(graph[node] - visited)
    return visited
```

### Key points 
- utilizes [queue](../datastructures.md#queue) data structure
- LIFO (last in, first out) 

### Complexity
- Time: O(V + E)
- Space: O(V)

## DFS
The depth-first search (DFS) algorithm is a graph traversal algorithm that starts at a given node and explores as far as possible along each branch before backtracking. It is implemented using a stack data structure.

### Pseudocode
```python
def dfs(start, graph):
    visited = set()
    stack = [start]

    while stack:
        node = stack.pop()
        if node not in visited:
            visited.add(node)
            stack.extend(graph[node] - visited)
    return visited
```

### Key points
- utilizes [stack](../datastructures.md#stack) data structure
- FIFO (first in, first out)

### Complexity
- Time: O(V + E)
- Space: O(V)

## A*
A* is a graph traversal algorithm that uses a heuristic function to find the shortest path between two nodes in a graph. It is implemented using a priority queue data structure.

### Pseudocode
```python
def a_star(start, goal, graph):
    visited = set()
    queue = [(0, start)]

    while queue:
        cost, node = heapq.heappop(queue)
        if node not in visited:
            visited.add(node)
            if node == goal:
                return cost
            for neighbor in graph[node]:
                heapq.heappush(queue, (cost + graph[node][neighbor], neighbor))
    return -1
```

### Key points
- utilizes [priority queue](../datastructures.md#priority-queue) data structure

### Complexity
- Time: O(V + E)
- Space: O(V)