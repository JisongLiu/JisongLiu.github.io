### Topologic sort

- add this node only when all nodes it points to have been added
- reverse when output

### Find the loop

#### Find the loop for undirectly graph

- Data structure: visit[], parentNode
- Traverse all the node (in case some nodes are not connected) if it hasn't been visited
- For each node, DFS it. If all it's child node haven't been visited expects its parent node and all of them don't have the loop,
return true.
- For each node, mark it as visited before entering next layer

#### Find the loop for directly graph

- Data structure: visit[], checked[]
- Traverse all the node (in case some nodes are not connected) if it hasn't been visited.
- For each node, return true 1) if it has been checked OR 2) all it's children have not been visited and all it's children 
don't have the loop
- For each node, mark it as visited before entering next layer and mark it as unvisited after jump out the current layer.
