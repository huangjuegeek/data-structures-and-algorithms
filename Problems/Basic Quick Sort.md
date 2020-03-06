基本的快速排序
```java
import java.util.Arrays;
import java.util.Random;

public class BasicQuickSort {

    private static Random rand = new Random();

    private static <T extends Comparable<T>> void swap(T[] arr, int index1, int index2) {
        T tmp = arr[index1];
        arr[index1] = arr[index2];
        arr[index2] = tmp;
    }

    private static <T extends Comparable<T>> int partition1(T[] arr, int left, int right) {
        T x = arr[right];    // 选最右边的元素作为枢轴
        int i = left - 1;
        for (int j = left; j < right; j++) {
            if (arr[j].compareTo(x) < 0) {
                i++;
                swap(arr, i, j);
            }
        }
        i++;
        swap(arr, i, right);
        return i;
    }

    private static <T extends Comparable<T>> int partition2(T[] arr, int left, int right) {
        if (arr == null || left < 0 || right >= arr.length) {
            throw new RuntimeException("Invalid Parameters!");
        }

        int pivot = rand.nextInt(right - left + 1) + left;    // 随机选取元素作为枢轴
        swap(arr, pivot, right);
        int i = left - 1;
        for (int j = left; j < right; j++) {
            if (arr[j].compareTo(arr[right]) < 0) {
                i++;
                if (i != j) {
                    swap(arr, i, j);
                }
            }
        }
        i++;
        swap(arr, i, right);
        return i;
    }

    private static <T extends Comparable<T>> int partition3(T[] arr, int left, int right) {
        int i = left, j = right;
        T x = arr[left];
        while (i < j) {
            while (i < j && arr[j].compareTo(x) >= 0) {
                j--;
            }
            if (i < j) {
                arr[i++] = arr[j];
            }
            while (i < j && arr[i].compareTo(x) <= 0) {
                i++;
            }
            if (i < j) {
                arr[j--] = arr[i];
            }
        }
        arr[i] = x;
        return i;
    }

    public static <T extends Comparable<T>> void quickSort(T[] arr, int left, int right) {
        if (arr == null || left < 0 || right >= arr.length) {
            throw new IllegalArgumentException();
        }

        if (left < right) {
            int p = partition2(arr, left, right);
            quickSort(arr, left, p - 1);
            quickSort(arr, p + 1, right);
        }
    }

    public static <T extends Comparable<T>> void testQuickSort(T[] arr) {
        System.out.println("before sorting: " + Arrays.toString(arr));
        if (arr != null) {
            quickSort(arr, 0, arr.length - 1);
            System.out.println(" after sorting: " + Arrays.toString(arr));
        }
    }

    public static void main(String[] args) throws Exception {
        Integer[] A = {34, 17, 93, 43, 66, 90, 32, 4, 78};
        testQuickSort(A);
        Integer[] B = {9, 9, 9, 9, 9, 9, 9, 9, 9, 9, 9};
        testQuickSort(B);
        Integer[] C = {-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5};
        testQuickSort(C);
        Integer[] D = {90, 81, 73, 43, 21, 18, 10, 5, 0, -9};
        testQuickSort(D);
        Integer[] E = {};
        testQuickSort(E);
        testQuickSort(null);
    }
}

OUTPUT:
before sorting: [34, 17, 93, 43, 66, 90, 32, 4, 78]
 after sorting: [4, 17, 32, 34, 43, 66, 78, 90, 93]
before sorting: [9, 9, 9, 9, 9, 9, 9, 9, 9, 9, 9]
 after sorting: [9, 9, 9, 9, 9, 9, 9, 9, 9, 9, 9]
before sorting: [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]
 after sorting: [-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]
before sorting: [90, 81, 73, 43, 21, 18, 10, 5, 0, -9]
 after sorting: [-9, 0, 5, 10, 18, 21, 43, 73, 81, 90]
before sorting: []
 after sorting: []
before sorting: null
```
