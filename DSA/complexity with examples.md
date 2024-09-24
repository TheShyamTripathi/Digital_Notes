Time complexity is a key aspect of analyzing algorithms in Data Structures and Algorithms (DSA). Below are examples of common time complexities in C programs, with explanations and example cases where each occurs:

### 1. **Constant Time – O(1)**
   - **Explanation**: The algorithm takes the same amount of time to complete, regardless of the input size.
   - **Example**: Accessing an element in an array by index.
     ```c
     int getElement(int arr[], int index) {
         return arr[index];  // O(1)
     }
     ```
   - **Use case**: Retrieving an element from an array.

### 2. **Logarithmic Time – O(log n)**
   - **Explanation**: The algorithm reduces the problem size by half with each step.
   - **Example**: Binary search.
     ```c
     int binarySearch(int arr[], int n, int key) {
         int low = 0, high = n - 1;
         while (low <= high) {
             int mid = (low + high) / 2;
             if (arr[mid] == key)
                 return mid;  // O(log n)
             else if (arr[mid] < key)
                 low = mid + 1;
             else
                 high = mid - 1;
         }
         return -1;
     }
     ```
   - **Use case**: Searching in a sorted array.

### 3. **Linear Time – O(n)**
   - **Explanation**: The time taken grows directly with the input size.
   - **Example**: Linear search.
     ```c
     int linearSearch(int arr[], int n, int key) {
         for (int i = 0; i < n; i++) {
             if (arr[i] == key)
                 return i;  // O(n)
         }
         return -1;
     }
     ```
   - **Use case**: Searching an unsorted array.

### 4. **Linearithmic Time – O(n log n)**
   - **Explanation**: This complexity is typical of efficient sorting algorithms.
   - **Example**: Merge Sort.
     ```c
     void merge(int arr[], int l, int m, int r) {
         int n1 = m - l + 1;
         int n2 = r - m;
         int L[n1], R[n2];
         for (int i = 0; i < n1; i++)
             L[i] = arr[l + i];
         for (int j = 0; j < n2; j++)
             R[j] = arr[m + 1 + j];
         int i = 0, j = 0, k = l;
         while (i < n1 && j < n2) {
             if (L[i] <= R[j]) {
                 arr[k] = L[i];
                 i++;
             } else {
                 arr[k] = R[j];
                 j++;
             }
             k++;
         }
         while (i < n1) {
             arr[k] = L[i];
             i++;
             k++;
         }
         while (j < n2) {
             arr[k] = R[j];
             j++;
             k++;
         }
     }

     void mergeSort(int arr[], int l, int r) {
         if (l < r) {
             int m = l + (r - l) / 2;
             mergeSort(arr, l, m);
             mergeSort(arr, m + 1, r);
             merge(arr, l, m, r);  // O(n log n)
         }
     }
     ```
   - **Use case**: Efficient sorting.

### 5. **Quadratic Time – O(n²)**
   - **Explanation**: The algorithm’s time increases quadratically with input size.
   - **Example**: Selection Sort.
     ```c
     void selectionSort(int arr[], int n) {
         int i, j, min_idx;
         for (i = 0; i < n-1; i++) {
             min_idx = i;
             for (j = i+1; j < n; j++)
                 if (arr[j] < arr[min_idx])
                     min_idx = j;
             int temp = arr[min_idx];
             arr[min_idx] = arr[i];
             arr[i] = temp;  // O(n²)
         }
     }
     ```
   - **Use case**: Basic sorting algorithms like bubble sort and insertion sort.

### 6. **Cubic Time – O(n³)**
   - **Explanation**: The time increases cubically with input size.
   - **Example**: A naive matrix multiplication.
     ```c
     void multiplyMatrix(int A[][N], int B[][N], int C[][N], int N) {
         for (int i = 0; i < N; i++) {
             for (int j = 0; j < N; j++) {
                 C[i][j] = 0;
                 for (int k = 0; k < N; k++) {
                     C[i][j] += A[i][k] * B[k][j];  // O(n³)
                 }
             }
         }
     }
     ```
   - **Use case**: Matrix operations.

### 7. **Exponential Time – O(2ⁿ)**
   - **Explanation**: Time doubles with every additional input element.
   - **Example**: Solving the Fibonacci sequence recursively.
     ```c
     int fib(int n) {
         if (n <= 1)
             return n;
         return fib(n-1) + fib(n-2);  // O(2ⁿ)
     }
     ```
   - **Use case**: Recursive algorithms like solving the Fibonacci series, the traveling salesman problem.

### 8. **Factorial Time – O(n!)**
   - **Explanation**: The time grows factorially with the input size.
   - **Example**: Solving the traveling salesman problem using brute-force recursion.
     ```c
     void tsp(int graph[][N], int pos, int visited, int cost, int N) {
         if (visited == ((1 << N) - 1)) {
             return cost + graph[pos][0];  // O(n!)
         }
         for (int i = 0; i < N; i++) {
             if (!(visited & (1 << i))) {
                 tsp(graph, i, visited | (1 << i), cost + graph[pos][i], N);
             }
         }
     }
     ```
   - **Use case**: Complex problems like the traveling salesman problem.

These examples demonstrate different time complexities that algorithms can have based on their design and structure.
