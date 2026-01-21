# Day 1 - Count Total Set Bits  (Bit Manipulation)

## 📌 Problem Statement
Given a positive integer **A**, count the **total number of set bits (1s)** in the binary representation of **all numbers from 1 to A**.

Return the result **modulo (10⁹ + 7)**.

---

## Approach (Efficient + Recursive)
Brute force counting bits for every number from `1...A` would be too slow because **A can go up to 10⁹**.

So we use a **pattern-based recursive solution**:

### Key Observations
1. Let `p = floor(log2(A))`  
   → `2^p` is the highest power of 2 ≤ A

2. Total set bits from **1 to (2^p - 1)** follows a known formula:
 p * 2^(p-1)

3. Remaining numbers from **2^p to A** contribute:
- MSB contributes `(A - 2^p + 1)` times
- Solve the rest recursively

---

##  Java Solution
```java
public class Solution {
 public int solve(int A) {
     int m = (int)(1e9 + 7);

     if (A <= 0) return 0;

     int p = (int)(Math.log(A) / Math.log(2));
     long ans = 0;

     // total set bits from 1 to (2^p - 1)
     ans = ((long)p * (1 << (p - 1))) % m;

     // MSB contribution from 2^p to A
     long x = (long)A - (1 << p) + 1;
     ans = (ans + x) % m;

     // recursive for remaining bits
     ans = (ans + solve((int)x - 1)) % m;

     return (int) ans;
 }
}
