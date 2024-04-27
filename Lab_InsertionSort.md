# Challenges
    Was not able to achieve the same output for comparisons

```java
public class Main {
    public static void insertionSort(int [] numbers) {
        int i;
        int j;
        int temp;      // Temporary variable for swap
        int swaps = 0, loops = 1;

        for (i = 1; i < numbers.length; ++i) {
            j = i;
            // Insert numbers[i] into sorted part
            // stopping once numbers[i] in correct position
            while (j > 0 && numbers[j] < numbers[j - 1]) {

                // Swap numbers[j] and numbers[j - 1]
                temp = numbers[j];
                numbers[j] = numbers[j - 1];
                numbers[j - 1] = temp;
                --j;
                swaps++;
            }
            for (int k = 0; k < numbers.length; ++k) {
                System.out.print(numbers[k] + " ");
            }
            System.out.println();
            loops++;
        }

        System.out.println("Comparisons: " + loops);
        System.out.println("Swaps: " + swaps);
    }

    public static void main(String [] args) {
        int [] numbers = {3, 2, 1, 5, 9, 8};
        int i;
        int comps = 0, loops = 0;

//        System.out.print("UNSORTED: ");
        for (i = 0; i < numbers.length; ++i) {
            System.out.print(numbers[i] + " ");
        }
        System.out.println();

        insertionSort(numbers);

//        System.out.print("SORTED: ");
//        for (i = 0; i < numbers.length; ++i) {
//            System.out.print(numbers[i] + " ");
//        }
//        System.out.println();

    }
}
```
