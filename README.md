# GitHub Classroom Assignments for Final Year Students

## Assignment 2: Social Media Network Analyzer

**Skills Tested:** Graph Algorithms, Object Manipulation, Recursion

**Difficulty:** Hard

### Problem Statement
Create a social network analysis tool that processes user connections, posts, and interactions.

### Requirements

1. **`findMutualFriends(userId1, userId2, network)`**
   - Return array of user IDs who are friends with both users
   - Optimize for large networks (10,000+ users)

2. **`calculateInfluenceScore(userId, network)`**
   - Score based on: followers count, engagement rate, friend connections
   - Formula: (followers × 0.5) + (avgLikesPerPost × 0.3) + (mutualConnections × 0.2)
   - Return normalized score (0-100)

3. **`findConnectionPath(userId1, userId2, network, maxDepth)`**
   - Find shortest connection path between two users
   - Return array of user IDs representing the path
   - Return null if no path exists within maxDepth

4. **`recommendFriends(userId, network, count)`**
   - Suggest friends based on mutual connections
   - Exclude existing friends and the user themselves
   - Return top N recommendations with relevance scores

5. **`detectCommunities(network, minSize)`**
   - Identify closely connected groups of users
   - Community = users with at least 50% connections within group
   - Return array of arrays (each inner array is a community)

### Sample Data Structure
```javascript
const network = {
  users: [
    {
      userId: "U001",
      name: "Alice",
      friends: ["U002", "U003", "U004"],
      followers: 1500,
      posts: [
        { postId: "P001", likes: 150, comments: 20 },
        { postId: "P002", likes: 200, comments: 35 }
      ]
    }
  ]
};
```

### Evaluation Criteria
- **Algorithm Correctness:** 35%
- **Complexity Analysis:** 25% - Must include Big-O analysis in comments
- **Code Organization:** 20% - Modular, reusable functions
- **Testing:** 20% - Comprehensive unit tests provided

## General Submission Guidelines for All Assignments

### Repository Structure
```
├── src/
│   ├── solution.js (or solution.py)
│   └── utils/ (helper functions)
├── tests/
│   └── solution.test.js
├── README.md (approach explanation)
├── COMPLEXITY.md (Big-O analysis)
└── package.json (or requirements.txt)
```

### Time Limit
- 60 minutes
