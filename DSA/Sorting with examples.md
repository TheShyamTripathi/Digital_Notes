Here’s a list of the most common sorting algorithms in computer science, their definitions, explanations, and C code examples:

---

### 1. **Bubble Sort**
   - **Definition**: A simple comparison-based algorithm that repeatedly swaps adjacent elements if they are in the wrong order.
   - **Explanation**: It repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. This process is repeated until the list is sorted.
   - **Time Complexity**: O(n²) for the worst and average cases; O(n) for the best case (already sorted).
   - **Example (C Code)**:
     ```c
     void bubbleSort(int arr[], int n) {
         for (int i = 0; i < n-1; i++) {
             for (int j = 0; j < n-i-1; j++) {
                 if (arr[j] > arr[j+1]) {
                     int temp = arr[j];
                     arr[j] = arr[j+1];
                     arr[j+1] = temp;
                 }
             }
         }
     }
     ```

---

### 2. **Selection Sort**
   - **Definition**: A comparison-based sorting algorithm where the smallest (or largest) element is selected from the unsorted portion and swapped with the first unsorted element.
   - **Explanation**: It repeatedly selects the smallest element from the unsorted part and moves it to the sorted part.
   - **Time Complexity**: O(n²) for all cases.
   - **Example (C Code)**:
     ```c
     void selectionSort(int arr[], int n) {
         for (int i = 0; i < n-1; i++) {
             int min_idx = i;
             for (int j = i+1; j < n; j++) {
                 if (arr[j] < arr[min_idx])
                     min_idx = j;
             }
             int temp = arr[min_idx];
             arr[min_idx] = arr[i];
             arr[i] = temp;
         }
     }
     ```

---

### 3. **Insertion Sort**
   - **Definition**: A comparison-based algorithm where elements are picked from an unsorted list and inserted into their correct position in the sorted part of the list.
   - **Explanation**: Works similarly to sorting playing cards. It builds a sorted array one item at a time by comparing each new element with the already sorted ones.
   - **Time Complexity**: O(n²) for the worst and average cases; O(n) for the best case.
   - **Example (C Code)**:
     ```c
     void insertionSort(int arr[], int n) {
         for (int i = 1; i < n; i++) {
             int key = arr[i];
             int j = i - 1;
             while (j >= 0 && arr[j] > key) {
                 arr[j + 1] = arr[j];
                 j = j - 1;
             }
             arr[j + 1] = key;
         }
     }
     ```

---

### 4. **Merge Sort**
   - **Definition**: A divide-and-conquer algorithm that divides the input array into two halves, recursively sorts them, and then merges the two sorted halves.
   - **Explanation**: It splits the array into two halves, sorts each half recursively, and merges the sorted halves to produce the final sorted array.
   - **Time Complexity**: O(n log n) for all cases.
   - **Example (C Code)**:
     ```c
     void merge(int arr[], int l, int m, int r) {
         int n1 = m - l + 1;
         int n2 = r - m;
         int L[n1], R[n2];
         for (int i = 0; i < n1; i++)
             L[i] = arr[l + i];
         for (int i = 0; i < n2; i++)
             R[i] = arr[m + 1 + i];

         int i = 0, j = 0, k = l;
         while (i < n1 && j < n2) {
             if (L[i] <= R[j])
                 arr[k++] = L[i++];
             else
                 arr[k++] = R[j++];
         }

         while (i < n1)
             arr[k++] = L[i++];

         while (j < n2)
             arr[k++] = R[j++];
     }

     void mergeSort(int arr[], int l, int r) {
         if (l < r) {
             int m = l + (r - l) / 2;
             mergeSort(arr, l, m);
             mergeSort(arr, m + 1, r);
             merge(arr, l, m, r);
         }
     }
     ```

---

### 5. **Quick Sort**
   - **Definition**: A divide-and-conquer algorithm that picks a "pivot" element and partitions the array around the pivot so that elements smaller than the pivot are on the left, and elements larger than the pivot are on the right.
   - **Explanation**: It recursively sorts the left and right halves of the pivot. The choice of pivot significantly affects performance.
   - **Time Complexity**: O(n²) for the worst case, O(n log n) for average and best cases.
   - **Example (C Code)**:
     ```c
     int partition(int arr[], int low, int high) {
         int pivot = arr[high];
         int i = (low - 1);
         for (int j = low; j <= high - 1; j++) {
             if (arr[j] < pivot) {
                 i++;
                 int temp = arr[i];
                 arr[i] = arr[j];
                 arr[j] = temp;
             }
         }
         int temp = arr[i + 1];
         arr[i + 1] = arr[high];
         arr[high] = temp;
         return (i + 1);
     }

     void quickSort(int arr[], int low, int high) {
         if (low < high) {
             int pi = partition(arr, low, high);
             quickSort(arr, low, pi - 1);
             quickSort(arr, pi + 1, high);
         }
     }
     ```

---

### 6. **Heap Sort**
   - **Definition**: A comparison-based sorting algorithm that uses a binary heap data structure. It repeatedly extracts the maximum element and moves it to the end of the array.
   - **Explanation**: First, the array is turned into a max-heap, then the largest element is swapped with the last element, and the heap size is reduced. The process is repeated for the rest of the elements.
   - **Time Complexity**: O(n log n) for all cases.
   - **Example (C Code)**:
     ```c
     void heapify(int arr[], int n, int i) {
         int largest = i;
         int l = 2 * i + 1;
         int r = 2 * i + 2;

         if (l < n && arr[l] > arr[largest])
             largest = l;

         if (r < n && arr[r] > arr[largest])
             largest = r;

         if (largest != i) {
             int temp = arr[i];
             arr[i] = arr[largest];
             arr[largest] = temp;
             heapify(arr, n, largest);
         }
     }

     void heapSort(int arr[], int n) {
         for (int i = n / 2 - 1; i >= 0; i--)
             heapify(arr, n, i);

         for (int i = n - 1; i > 0; i--) {
             int temp = arr[0];
             arr[0] = arr[i];
             arr[i] = temp;
             heapify(arr, i, 0);
         }
     }
     ```

---

### 7. **Radix Sort**
   - **Definition**: A non-comparison-based sorting algorithm that sorts numbers digit by digit, starting from the least significant digit to the most significant digit.
   - **Explanation**: Radix sort processes the numbers digit by digit, usually using another stable sort (such as counting sort) for each digit.
   - **Time Complexity**: O(d * (n + k)) where `d` is the number of digits in the largest number and `k` is the range of the digit values.
   - **Example (C Code)**:
     ```c
     int getMax(int arr[], int n) {
         int max = arr[0];
         for (int i = 1; i < n; i++)
             if (arr[i] > max)
                 max = arr[i];
         return max;
     }

     void countSort(int arr[], int n, int exp) {
         int output[n];
         int count[10] = {0};
         for (int i = 0; i < n; i++)
             count[(arr[i] / exp) % 10]++;
         for (int i = 1; i < 10; i++)
             count[i] += count[i - 1];
         for (int i = n - 1; i >= 0; i--) {
             output[count[(arr[i] / exp) % 10] - 1] = arr[i];
             count[(arr[i] / exp) % 10]--;
         }
         for (int i = 0; i < n; i++)
             arr[i] = output[i];
     }

     void radixSort(int arr[], int n) {
         int

 max = getMax(arr, n);
         for (int exp = 1; max / exp > 0; exp *= 10)
             countSort(arr, n, exp);
     }
     ```

---

### 8. **Counting Sort**
   - **Definition**: A non-comparison-based sorting algorithm that counts the occurrence of each unique element and uses this count to place elements in the correct position.
   - **Explanation**: It creates a count array and uses it to calculate the positions of elements in the sorted array.
   - **Time Complexity**: O(n + k) where `k` is the range of input values.
   - **Example (C Code)**:
     ```c
     void countingSort(int arr[], int n, int range) {
         int count[range + 1], output[n];
         memset(count, 0, sizeof(count));

         for (int i = 0; i < n; i++)
             count[arr[i]]++;

         for (int i = 1; i <= range; i++)
             count[i] += count[i - 1];

         for (int i = n - 1; i >= 0; i--) {
             output[count[arr[i]] - 1] = arr[i];
             count[arr[i]]--;
         }

         for (int i = 0; i < n; i++)
             arr[i] = output[i];
     }
     ```

---

### 9. **Bucket Sort**
   - **Definition**: A non-comparison-based sorting algorithm that distributes elements into several buckets, sorts them individually, and then merges them.
   - **Explanation**: The algorithm distributes elements into buckets, sorts each bucket (often using insertion sort or another simple algorithm), and then merges the results.
   - **Time Complexity**: O(n + k), where `n` is the number of elements and `k` is the number of buckets.
   - **Example (C Code)**:
     ```c
     void bucketSort(float arr[], int n) {
         vector<float> buckets[n];
         for (int i = 0; i < n; i++) {
             int idx = n * arr[i];
             buckets[idx].push_back(arr[i]);
         }

         for (int i = 0; i < n; i++)
             sort(buckets[i].begin(), buckets[i].end());

         int index = 0;
         for (int i = 0; i < n; i++)
             for (int j = 0; j < buckets[i].size(); j++)
                 arr[index++] = buckets[i][j];
     }
     ```

---

These examples cover a wide range of sorting algorithms, including both comparison-based and non-comparison-based methods, with varying time complexities and use cases.
