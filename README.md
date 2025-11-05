# GitHub Classroom Assignment

## Assignment 1: E-Commerce Data Analytics Dashboard

### Problem Statement
Build a data processing system for an e-commerce platform that analyzes customer orders, products, and sales data.

### Requirements
Students must implement the following functions:

1. **`getTopSellingProducts(orders, n)`**
   - Return top N products by total quantity sold
   - Handle ties appropriately
   - Time complexity: O(n log n) or better

2. **`calculateRevenueByCategory(orders, products)`**
   - Group revenue by product categories
   - Return sorted object with category totals
   - Include percentage of total revenue

3. **`findCustomerSegments(customers, orders)`**
   - Segment customers into: VIP (>$10k spent), Regular ($1k-$10k), New (<$1k)
   - Return object with arrays of customer IDs per segment
   - Calculate average order value per segment

4. **`getMonthlyTrends(orders, startDate, endDate)`**
   - Aggregate orders by month within date range
   - Return array of objects with month, revenue, order count
   - Handle edge cases (no orders in a month)

5. **`mergeAndDeduplicateProducts(productsArray1, productsArray2)`**
   - Merge two product catalogs
   - Remove duplicates based on product ID
   - Keep most recent data when conflicts exist

### Sample Data Structure
```javascript
const orders = [
  {
    orderId: "ORD001",
    customerId: "CUST123",
    products: [
      { productId: "P001", quantity: 2, price: 29.99 },
      { productId: "P002", quantity: 1, price: 49.99 }
    ],
    orderDate: "2024-01-15",
    totalAmount: 109.97
  }
];

const products = [
  {
    productId: "P001",
    name: "Wireless Mouse",
    category: "Electronics",
    price: 29.99
  }
];
```

### Evaluation Criteria
- **Correctness:** 40% - All test cases pass
- **Code Quality:** 25% - Clean, readable code with proper naming
- **Efficiency:** 20% - Optimal time/space complexity
- **Edge Cases:** 15% - Handles empty arrays, null values, invalid data

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
