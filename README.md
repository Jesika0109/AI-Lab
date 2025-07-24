def iterative_deepening_search(graph, start, goal, limit):


    def dfs_at_depth(node, depth, path):
        
        
        if depth > limit:
            return None  # If depth limit exceeded, stop searching
        
        path.append(node)  # Add current node to the path
        
        if node == goal:
            return path  # If goal is found, return the path
        
        for neighbor in graph.get(node, []):
            if neighbor not in path:  # Avoid cycles
                result = dfs_at_depth(neighbor, depth + 1, path.copy())
                if result:
                    return result
        
        return None  # Return None if no path found at this depth

    # Iteratively increase the depth limit
    for depth in range(limit + 1):
        print(f"Searching at depth {depth}...")
        result = dfs_at_depth(start, 0, [])
        if result:  # If goal is found at any depth, return the result
            return result

    return None  # If goal is not found within the depth limit


# Example usage:
if __name__ == "__main__":
    # Graph as adjacency list
    graph = {
        'A': ['B', 'C'],
        'B': ['A', 'D', 'E'],
        'C': ['A', 'F'],
        'D': ['B'],
        'E': ['B', 'F'],
        'F': ['C', 'E']
    }

    # User input for the goal and depth limit
    start_node = input("Enter the start node: ")
    goal_node = input("Enter the goal node: ")
    depth_limit = int(input("Enter the depth limit: "))

    # Call the iterative deepening search algorithm
    result = iterative_deepening_search(graph, start_node, goal_node, depth_limit)

    # Output the result
    if result:
        print(f"Path to goal {goal_node}: {result}")
    else:
        print(f"No path found to goal {goal_node} within the depth limit of {depth_limit}.")
