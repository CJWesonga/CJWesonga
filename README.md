import heapq

def dijkstra(graph, start_node):
    distances = {node: float('inf') for node in graph}
    distances[start_node] = 0
    priority_queue = [(0, start_node)]  # (distance, node)

    while priority_queue:
        current_distance, current_node = heapq.heappop(priority_queue)

        # Ignore outdated entries in the priority queue
        if current_distance > distances[current_node]:
            continue

        for neighbor, weight in graph.get(current_node, {}).items():
            distance = current_distance + weight
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(priority_queue, (distance, neighbor))

    return distances

# Example usage:
graph = {
    'A': {'B': 1, 'C': 4},
    'B': {'A': 1, 'D': 3, 'E': 7},
    'C': {'A': 4, 'F': 2},
    'D': {'B': 3, 'E': 1},
    'E': {'B': 7, 'D': 1, 'F': 5},
    'F': {'C': 2, 'E': 5}
}

start_node = 'A'
shortest_paths = dijkstra(graph, start_node)
print(f"Shortest paths from node '{start_node}': {shortest_paths}")
