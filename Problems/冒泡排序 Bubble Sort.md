# 冒泡排序 Bubble Sort
```java
import java.util.Arrays;

public class BubbleSort {

    /**
     * 针对泛型的冒泡排序
     *
     * @param A   待排序数组
     * @param <T> 待排序数组中元素的类型参数
     */
    public static <T extends Comparable<? super T>> void bubbleSort(T[] A) {
        int i, j;
        boolean swapFlag; //该趟排序过程是否发生了交换的标识

        for (i = A.length - 1; i > 0; i--) {
            swapFlag = false;
            for (j = 0; j < i; j++) {
                //如果第j个元素大于第j+1个元素，则交换它们
                if (A[j].compareTo(A[j + 1]) > 0) {
                    T tmp = A[j];
                    A[j] = A[j + 1];
                    A[j + 1] = tmp;
                    swapFlag = true;
                }
            }
            //如果该趟未发生交换，则表明整个数组已经处于有序状态，可以提前结束循环
            if (!swapFlag) {
                break;
            }
        }
    }

    /**
     * 针对整型数组的冒泡排序
     *
     * @param A 待排序数组
     */
    public static void bubbleSort(int[] A) {
        int i, j;
        boolean swapFlag;

        for (i = A.length - 1; i > 0; i--) {
            swapFlag = false;
            for (j = 0; j < i; j++) {
                if (A[j] > A[j + 1]) {
                    int tmp = A[j];
                    A[j] = A[j + 1];
                    A[j + 1] = tmp;
                    swapFlag = true;
                }
            }
            if (!swapFlag) {
                break;
            }
        }
    }

    public static void main(String[] args) {
        int[] A = {34, 17, 93, 43, 66, 90, 32, 4, 78, 17};
        Integer[] B = new Integer[A.length];
        for (int i = 0; i < B.length; i++) {
            B[i] = A[i];
        }

        System.out.println("before sort: " + Arrays.toString(A));
        bubbleSort(A);
        System.out.println("after sort: " + Arrays.toString(A));

        System.out.println();

        System.out.println("before sort: " + Arrays.toString(B));
        bubbleSort(B);
        System.out.println("after sort: " + Arrays.toString(B));
    }
}
```
