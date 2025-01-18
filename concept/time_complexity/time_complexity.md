
# Time Complexity

In terms of time complexity, the performance of algorithms can be ranked based on their growth rates. The following order lists complexities from fastest to slowest (left to right indicates increasing execution time as input size \(n\) grows):

1. **\(O(1)\)**: Constant time
   - The execution time remains the same regardless of input size.
   - Example: Accessing a specific index in an array.

2. **\(O(\log n)\)**: Logarithmic time
   - The execution time grows slowly as the input size increases.
   - Example: Binary search.

3. **\(O(n)\)**: Linear time
   - The execution time grows proportionally with the input size.
   - Example: Iterating through all elements in an array.

4. **\(O(n \log n)\)**: Linearithmic time
   - The execution time grows faster than \(O(n)\) but slower than \(O(n^2)\).
   - Example: Efficient sorting algorithms like quicksort or merge sort.

5. **\(O(n^2)\)**: Quadratic time
   - The execution time grows proportionally to the square of the input size.
   - Example: Nested loops, such as in bubble sort or selection sort.

6. **\(O(n^3)\)**: Cubic time
   - The execution time grows proportionally to the cube of the input size.
   - Example: Algorithms with three nested loops.

7. **\(O(2^n)\)**: Exponential time
   - The execution time increases dramatically with the input size.
   - Example: Recursive algorithms that explore all subsets.

8. **\(O(n!)\)**: Factorial time
   - The execution time grows the fastest, becoming impractical for even small input sizes.
   - Example: Generating all permutations of \(n\) elements.

### Summary of Time Complexity Order:
\[
O(1) \ < \ O(\log n) \ < \ O(n) \ < \ O(n \log n) \ < \ O(n^2) \ < \ O(n^3) \ < \ O(2^n) \ < \ O(n!)
\]

When designing or choosing an algorithm, aim for efficient complexities like \(O(1)\), \(O(\log n)\), \(O(n)\), or \(O(n \log n)\), especially when handling large input sizes.




Here is the graph showing the growth rates of various time complexities. The y-axis is in logarithmic scale to better visualize the differences between the complexities. 

## Time Complexity Graph
![Time Complexity Graph](https://raw.githubusercontent.com/kyungtaek-jonas-lim/jonastudy/main/concept/time_complexity/time_complexity_graph.png)


- **\(O(1)\):** Constant line, unaffected by input size.
- **\(O(\log n)\):** Grows slowly even as \(n\) increases.
- **\(O(n)\):** Linear growth with input size.
- **\(O(n \log n)\):** Slightly faster growth than \(O(n)\).
- **\(O(n^2)\):** Quadratic growth, increasing significantly for large \(n\).
- **\(O(n^3)\):** Even faster cubic growth.
- **\(O(2^n)\):** Exponential growth, rapidly increasing.
- **\(O(n!)\):** Factorial growth, skyrocketing for even small \(n\).

This graph highlights how critical it is to choose efficient algorithms, especially for larger input sizes.