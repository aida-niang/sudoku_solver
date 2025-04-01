# Explanation of Sudoku Solving Algorithms

## 1. Problem Modelling

A Sudoku is a 9×9 grid where each cell contains a number between 1 and 9, or is empty (denoted by 0). The goal is to fill the grid while respecting the following rules:

- **Each row** must contain the numbers 1 to 9 without repetition.
- **Each column** must contain the numbers 1 to 9 without repetition.
- **Each 3x3 subgrid** must contain the numbers 1 to 9 without repetition.

Mathematically, this means we are looking for a **matrix \( M \in \mathbb{N}^{9 \times 9} \)** such that:

\[
\forall i, j, k \in \{1, \dots, 9\}, \quad M_{i,j} = k \quad \text{if and only if this choice satisfies the above constraints}.
\]

In other words, each element of the matrix, \( M_{i,j} \), must satisfy the following three rules:

- A number must appear only once per row \( i \),
- A number must appear only once per column \( j \),
- A number must appear only once in each 3x3 subgrid.

## 2. Backtracking Algorithm

### General Idea

**Backtracking** is a systematic search method that explores the solution space exhaustively, but it "backs up" when it hits an impasse. It is a **recursive** algorithm where, after trying a number, it decides whether the choice is valid and, if not, tries another option.

### Mathematical Complexity

In the worst case, there are **81 cells to fill**, each with up to **9 possible choices**, giving an exponential complexity of \( O(9^{81}) \).

However, in practice, filtering out invalid choices (e.g., checking if a number respects Sudoku rules) significantly reduces the number of solutions to test. If, on average, each cell has \( k \) possible choices (typically \( k \approx 5 \)), the complexity becomes approximately \( O(k^n) \), with \( n \leq 81 \).

Thus, **backtracking** is much faster than brute force.

### Implementation

1. Find the first empty cell.
2. Try inserting a valid number (from 1 to 9).
3. If the choice is valid, recursively solve the remaining grid.
4. If no valid choice exists, backtrack and try another number.
5. If no valid choice works, backtrack to the previous cell.

This process guarantees finding a solution if one exists, although it may take some time depending on the difficulty of the grid.

## 3. Brute Force Algorithm

### General Idea

The **brute force** algorithm attempts **all possible combinations** to fill the grid without any optimization. It is an **exhaustive enumeration** method that explores all configurations without pre-filtering solutions.

### Mathematical Complexity

In the worst case, the brute force algorithm tests all possible combinations, which is \( 9^{81} \). This complexity is **too high** to be practical and thus is not feasible for large Sudoku grids.

In comparison to backtracking, where the complexity is \( O(k^n) \) with \( k < 9 \), brute force remains \( O(9^n) \), demonstrating an **exponential improvement** in efficiency for backtracking.

### Implementation

1. Fill each empty cell with a number between 1 and 9.
2. Check if the resulting grid is valid.
3. If valid, continue; otherwise, restart with another combination.
4. If no valid arrangement works in a reasonable time, the algorithm gives up.

Due to its inefficiency, this algorithm should only be used for **very small grids** or in simple cases.

## 4. Comparison and Mathematical Demonstration

To better understand why backtracking is faster, let's compare the two approaches in terms of exponential complexity:

\[
\frac{O(k^n)}{O(9^n)} = O\left( \left( \frac{k}{9} \right)^n \right)
\]

With \( k < 9 \), the ratio \( \left( \frac{k}{9} \right)^n \) becomes exponentially small, showing that **backtracking** is **much faster** than brute force.

### Comparison Table:

| Criterion            | **Backtracking**                        | **Brute Force**                    |
|----------------------|-----------------------------------------|------------------------------------|
| **Efficiency**        | Good                                    | Very low                          |
| **Complexity**        | \( O(k^n) \) with \( k < 9 \)           | \( O(9^n) \)                       |
| **Exponential Improvement** | Yes, with \( \left( \frac{k}{9} \right)^n \) | None                             |
| **Practical Use**     | Yes, commonly used for Sudoku solving   | No, too slow                      |

## 5. Conclusion

- **Backtracking** is an efficient method for solving Sudoku because it **reduces the search space** by quickly eliminating invalid choices. It can be used on standard Sudoku grids without major performance issues.
- **Brute Force**, on the other hand, is **much slower** and is practically unsuitable for solving large or full Sudoku grids.

In conclusion, **backtracking is the algorithm of choice** for efficiently solving Sudoku, while brute force is generally considered impractical for realistic Sudoku grids.

"""

