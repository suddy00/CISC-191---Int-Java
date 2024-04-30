# Challenges
  Required more data points than the Insertion sort

```java
public class Main {
        public static int merge(int [] numbers, int i, int j, int k) {
            int mergedSize = k - i + 1;       // Size of merged partition
            int[] mergedNumbers = new int[mergedSize]; // Temporary array for merged numbers
            int mergePos;                     // Position to insert merged number
            int leftPos;                      // Position of elements in left partition
            int rightPos;                     // Position of elements in right partition
            int comps = 0;

            mergePos = 0;
            leftPos = i;                      // Initialize left partition position
            rightPos = j + 1;                 // Initialize right partition position

            // Add the smallest element from left or right partition to merged numbers
            while (leftPos <= j && rightPos <= k) {
                if (numbers[leftPos] < numbers[rightPos]) {
                    mergedNumbers[mergePos] = numbers[leftPos];
                    ++leftPos;
                    comps++;
                }
                else {
                    mergedNumbers[mergePos] = numbers[rightPos];
                    ++rightPos;
                }
                ++mergePos;
            }

            // If left partition is not empty, add remaining elements to merged numbers
            while (leftPos <= j) {
                mergedNumbers[mergePos] = numbers[leftPos];
                ++leftPos;
                ++mergePos;
            }

            // If right partition is not empty, add remaining elements to merged numbers
            while (rightPos <= k) {
                mergedNumbers[mergePos] = numbers[rightPos];
                ++rightPos;
                ++mergePos;
            }

            // Copy merge number back to numbers
            for (mergePos = 0; mergePos < mergedSize; ++mergePos) {
                numbers[i + mergePos] = mergedNumbers[mergePos];
            }
            return comps;
        }

        public static int mergeSort(int [] numbers, int i, int k) {
            int j;
            int c=0;

            if (i < k) {
                c++;
                j = (i + k) / 2;  // Find the midpoint in the partition
                // Recursively sort left and right partitions
                mergeSort(numbers, i, j);
                mergeSort(numbers, j + 1, k);

                // Merge left and right partition in sorted order
                c+= merge(numbers, i, j, k);
            }
            return c;
        }

        public static void main(String [] args) {
            int [] numbers = {6, 3, 2, 1, 5, 9, 8};
            int i;

            System.out.print("UNSORTED: ");
            for (i = 0; i < numbers.length; ++i) {
                System.out.print(numbers[i] + " ");
            }
            System.out.println();

            /* initial call to merge sort with index */
            int comps = mergeSort(numbers, 0, numbers.length - 1);

            System.out.print("SORTED: ");
            for (i = 0; i < numbers.length; ++i) {
                System.out.print(numbers[i] + " ");
            }
            System.out.println();
            System.out.print("Comparisons: " + comps);
        }

}
```
