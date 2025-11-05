# Complexity Analysis

This document provides Big-O complexity analysis for all functions in the E-Commerce Data Analytics Dashboard.

## Notation
- `n` = number of orders
- `m` = number of products in an order (average)
- `p` = total number of unique products
- `c` = number of customers
- `k` = number of months in date range

---

## 1. `getTopSellingProducts(orders, n)`

### Time Complexity: **O(n·m + p log p)**
- **Iterate through orders:** O(n) - iterate through all orders
- **Iterate through products in each order:** O(n·m) - for each order, iterate through its products
- **Aggregate quantities:** O(p) - create/update product quantity map
- **Sort products:** O(p log p) - sort products by quantity to get top N
- **Select top N:** O(n) - extract top N products (or O(p) if using heap)

**Optimized approach:** O(n·m + p log n) using a min-heap of size N

### Space Complexity: **O(p)**
- **Product quantity map:** O(p) - store quantity for each unique product
- **Sorting overhead:** O(p) - for sorting algorithm
- **Result array:** O(n) - top N products (where N ≤ p)

---

## 2. `calculateRevenueByCategory(orders, products)`

### Time Complexity: **O(n·m + p + c log c)**
- **Build product lookup map:** O(p) - create map of productId → category
- **Iterate through orders:** O(n) - process each order
- **Iterate through products in orders:** O(n·m) - for each order, iterate through its products
- **Calculate revenue by category:** O(n·m) - aggregate revenue by category
- **Sort categories:** O(c log c) - sort categories (where c = number of categories, typically c << p)
- **Calculate percentages:** O(c) - calculate percentage of total revenue

**Note:** If products array is already a map/dictionary, product lookup becomes O(1) instead of O(p)

### Space Complexity: **O(c + p)**
- **Product lookup map:** O(p) - map of productId → category
- **Category revenue map:** O(c) - store revenue per category
- **Result object:** O(c) - sorted categories with revenue and percentages

---

## 3. `findCustomerSegments(customers, orders)`

### Time Complexity: **O(n·m + c)**
- **Build customer spending map:** O(n·m) - iterate through all orders and products to calculate total spending per customer
- **Iterate through customers:** O(c) - process each customer to assign segment
- **Calculate averages:** O(c) - calculate average order value per segment

**Alternative approach:** If using a customer lookup map, O(n·m + c)

### Space Complexity: **O(c)**
- **Customer spending map:** O(c) - store total spending per customer
- **Segment arrays:** O(c) - arrays of customer IDs per segment (all customers distributed)
- **Result object:** O(c) - segments with customer IDs and averages

---

## 4. `getMonthlyTrends(orders, startDate, endDate)`

### Time Complexity: **O(n + k)**
- **Filter orders by date range:** O(n) - iterate through orders to filter by date
- **Group by month:** O(n) - iterate through filtered orders and group by month
- **Calculate monthly aggregates:** O(k) - calculate revenue and order count per month
- **Handle missing months:** O(k) - fill in months with no orders (if needed)

**Note:** Date parsing and comparison is typically O(1) per operation

### Space Complexity: **O(k)**
- **Monthly trends map:** O(k) - store data for each month in range
- **Result array:** O(k) - array of monthly trend objects

---

## 5. `mergeAndDeduplicateProducts(productsArray1, productsArray2)`

### Time Complexity: **O(p₁ + p₂)**
- **Build lookup map from first array:** O(p₁) - create map of productId → product
- **Process second array:** O(p₂) - iterate through second array
  - **Check for duplicates:** O(1) - lookup in map
  - **Resolve conflicts:** O(1) - keep most recent data
- **Convert map to array:** O(p) - where p = unique products (p ≤ p₁ + p₂)

**Optimized approach:** O(p₁ + p₂) using hash map for deduplication

### Space Complexity: **O(p)**
- **Product lookup map:** O(p) - map of productId → product (stores unique products)
- **Result array:** O(p) - merged and deduplicated product array

---

## Summary Table

| Function | Time Complexity | Space Complexity | Dominant Factor |
|----------|----------------|------------------|-----------------|
| `getTopSellingProducts` | O(n·m + p log p) | O(p) | Sorting products |
| `calculateRevenueByCategory` | O(n·m + p + c log c) | O(c + p) | Order iteration |
| `findCustomerSegments` | O(n·m + c) | O(c) | Order processing |
| `getMonthlyTrends` | O(n + k) | O(k) | Order filtering |
| `mergeAndDeduplicateProducts` | O(p₁ + p₂) | O(p) | Array processing |

---

## Optimizations Considered

1. **`getTopSellingProducts`**: Can be optimized to O(n·m + p log n) using a min-heap of size N instead of sorting all products.

2. **`calculateRevenueByCategory`**: If products array is pre-processed into a map, lookup time reduces from O(p) to O(1), making overall complexity O(n·m + c log c).

3. **All functions**: Using Map/Set data structures for O(1) lookups instead of arrays improves performance for lookups and deduplication.
