# Complexity Analysis

## Big-O Analysis for Social Media Network Analyzer Functions

This document provides detailed time and space complexity analysis for each function in the Social Media Network Analyzer.

### Notation
- **V** = Total number of users (vertices) in the network
- **E** = Total number of edges (friendship connections) in the network
- **F₁** = Number of friends for userId1
- **F₂** = Number of friends for userId2
- **P** = Average number of posts per user
- **C** = Number of recommendations requested (count parameter)
- **D** = Maximum depth for path search (maxDepth parameter)

---

## 1. `findMutualFriends(userId1, userId2, network)`

### Time Complexity: **O(F₁ + F₂)**
- **Best Case:** O(min(F₁, F₂)) when using early termination
- **Average Case:** O(F₁ + F₂)
- **Worst Case:** O(F₁ + F₂)

**Analysis:**
- Finding user1 and user2 in the network: O(V) using linear search, or O(1) if using a hash map
- Creating a Set from user1's friends: O(F₁)
- Iterating through user2's friends and checking membership: O(F₂)
- Set lookup is O(1) on average
- **Optimization:** Using a Set/HashSet for O(1) lookup instead of array includes() which is O(F₁)

**For large networks (10,000+ users):**
- Use hash map for O(1) user lookup: O(V) preprocessing, then O(1) per query
- Use Set data structure for friend lists: O(1) membership testing

### Space Complexity: **O(F₁)**
- Set storing user1's friends: O(F₁)
- Result array: O(min(F₁, F₂)) in worst case (when all friends are mutual)

---

## 2. `calculateInfluenceScore(userId, network)`

### Time Complexity: **O(V + P)**
- **Best Case:** O(1) if user is found via hash map and has no posts
- **Average Case:** O(V + P)
- **Worst Case:** O(V + P)

**Analysis:**
- Finding user in network: O(V) with linear search, or O(1) with hash map
- Iterating through posts to calculate average likes: O(P)
- Calculating mutual connections: O(F) where F is the number of friends
  - For each friend, checking if they're friends with others: O(F × V) in naive approach
  - Optimized: O(F) if we just count connections
- All calculations are O(1) after data retrieval

### Space Complexity: **O(1)**
- Only storing scalar values (counters, totals)
- No additional data structures proportional to input size

---

## 3. `findConnectionPath(userId1, userId2, network, maxDepth)`

### Time Complexity: **O(V + E)**
- **Best Case:** O(1) if users are direct friends
- **Average Case:** O(V + E) for BFS up to maxDepth
- **Worst Case:** O(V + E) when exploring all nodes within maxDepth

**Analysis:**
- Uses Breadth-First Search (BFS) to find shortest path
- Each node is visited at most once: O(V)
- Each edge is traversed at most once: O(E)
- maxDepth limits the search, potentially reducing complexity
- **Total:** O(V + E) where E can be up to O(V²) in dense graphs

**Optimization Notes:**
- BFS guarantees shortest path (unweighted graph)
- Early termination when target is found
- maxDepth prevents infinite exploration

### Space Complexity: **O(V)**
- Queue storing nodes to visit: O(V) in worst case
- Visited set: O(V)
- Path reconstruction: O(D) where D ≤ maxDepth ≤ V

---

## 4. `recommendFriends(userId, network, count)`

### Time Complexity: **O(V × F_avg + C × log(V))**
- **Best Case:** O(V × F_avg) when sorting is not needed
- **Average Case:** O(V × F_avg + V × log(V))
- **Worst Case:** O(V × F_avg + V × log(V))

**Analysis:**
- Finding the user: O(V) or O(1) with hash map
- For each potential friend (V-1 users):
  - Calculate mutual connections: O(F_avg) where F_avg is average friends per user
  - Total: O(V × F_avg)
- Sorting recommendations by score: O(V × log(V))
- Selecting top C: O(C)
- **Total:** O(V × F_avg + V × log(V))

**Optimization:**
- Use priority queue (heap) to get top C: O(V × F_avg + C × log(V))
- Only calculate scores for potential friends (exclude existing friends)

### Space Complexity: **O(V)**
- Array storing all potential recommendations: O(V)
- Priority queue: O(V) in worst case
- Result array: O(C)

---

## 5. `detectCommunities(network, minSize)`

### Time Complexity: **O(V² × F_avg)**
- **Best Case:** O(V²) for sparse graphs
- **Average Case:** O(V² × F_avg)
- **Worst Case:** O(V² × F_avg) or O(V³) in dense graphs

**Analysis:**
- This is a community detection problem (similar to finding cliques or connected components)
- For each user O(V):
  - Check connections with other users: O(V)
  - Verify 50% connection threshold: O(F_avg)
  - Total per user: O(V × F_avg)
- **Total:** O(V² × F_avg)

**Alternative Approaches:**
- **Union-Find (Disjoint Set):** O(V × α(V)) where α is inverse Ackermann function (nearly constant)
- **DFS/BFS approach:** O(V + E) for finding connected components, then filtering
- **Greedy modularity:** O(V² × log(V)) for more sophisticated community detection

**Note:** The 50% connection threshold requires checking each pair's connection status, which is expensive.

### Space Complexity: **O(V²)**
- Adjacency matrix (if precomputed): O(V²)
- Community groups: O(V) in worst case (each user is a community)
- Visited tracking: O(V)

---

## Overall Network Operations

### Preprocessing Optimization
If we preprocess the network:
- **Build adjacency list:** O(V + E)
- **Build user lookup hash map:** O(V)
- **Build friend Set for each user:** O(V + E)

**Total preprocessing:** O(V + E)

After preprocessing:
- User lookup: O(1) instead of O(V)
- Friend membership check: O(1) instead of O(F)

---

## Summary Table

| Function | Time Complexity | Space Complexity | Optimization Priority |
|----------|----------------|------------------|----------------------|
| `findMutualFriends` | O(F₁ + F₂) | O(F₁) | High (use Set) |
| `calculateInfluenceScore` | O(V + P) | O(1) | Medium (hash map for user lookup) |
| `findConnectionPath` | O(V + E) | O(V) | Medium (BFS is optimal) |
| `recommendFriends` | O(V × F_avg + V × log(V)) | O(V) | High (use heap for top-K) |
| `detectCommunities` | O(V² × F_avg) | O(V²) | Critical (consider Union-Find) |

---

## Scalability Considerations

For networks with **10,000+ users**:

1. **Use hash-based data structures** for O(1) lookups
2. **Preprocess adjacency lists** instead of scanning arrays
3. **Limit depth** in path-finding algorithms
4. **Use efficient sorting** (heap) for top-K recommendations
5. **Consider approximate algorithms** for community detection on very large networks
