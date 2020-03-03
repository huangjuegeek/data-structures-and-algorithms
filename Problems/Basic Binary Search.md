基本的二分查找实现
```java
import java.util.Arrays;

public class BinarySearchTest {

    private final static int NOT_FOUND = -1;

    public static <T extends Comparable<? super T>> int binarySearch(T[] array, T target) {
        int low = 0;
        int high = array.length - 1;
        while (low <= high) {
            int mid = (low + high) >> 1;    // 相当于(low+high)/2，但效率更高
            if (target.compareTo(array[mid]) > 0) {
                low = mid + 1;
            } else if (target.compareTo(array[mid]) < 0) {
                high = mid - 1;
            } else {
                return mid;
            }
        }
        return NOT_FOUND;
    }

    public static void main(String[] args) {
        // 已经有序的，可以使用下面的方式，进行二分查找。
        Integer[] intArray = new Integer[]{2, 5, 8, 15, 24, 32, 45, 255, 452};
        Double[] doubleArray = new Double[]{2.0, 5.0, 8.0, 15.0, 24.0, 32.0, 45.0, 255.0, 452.0};
        String[] stringArray = new String[]{"ab", "bc", "cd", "de", "ef", "fg", "gh", "hi", "ij"};
        Student[] studentArray = new Student[]{
                new Student(1, "q"),
                new Student(2, "i"),
                new Student(3, "u"),
                new Student(4, "h"),
                new Student(5, "a"),
                new Student(6, "i"),
                new Student(7, "s"),
                new Student(8, "e"),
                new Student(9, "n")};

        int targetPos = BinarySearchTest.binarySearch(intArray, 255);
        System.out.println("查找Integer数组中的数的位置为：" + targetPos);
        targetPos = BinarySearchTest.binarySearch(doubleArray, 255.0);
        System.out.println("查找Double数组中的数的位置为：" + targetPos);
        // 查看String的java源码其中String实现了Comparable接口，所以这里可以使用
        // 这是java源码中的一段代码：public final class String implements
        // java.io.Serializable, Comparable<String>, CharSequence
        targetPos = BinarySearchTest.binarySearch(stringArray, "hi");
        System.out.println("查找String数组中的数的位置为：" + targetPos);
        targetPos = BinarySearchTest.binarySearch(studentArray, new Student(8));
        System.out.println("查找Student数组中的对象的内容为：" + studentArray[targetPos].toString());

        // 如果，还没有排序，即为乱序的话，可以通过java的Array的库方法sort进行排序。
        Integer[] intArray2 = new Integer[]{2, 5, 24, 45, 32, 452, 255, 8, 15};
        Arrays.sort(intArray2);
        targetPos = BinarySearchTest.binarySearch(intArray2, 255);
        System.out.println("先通过排序，然后查找Integer数组中的数的位置为：" + targetPos);
    }
}

class Student implements Comparable<Student> {

    int stuNo;
    String stuName;

    public Student() {
    }

    public Student(int stuNo, String stuName) {
        this.stuNo = stuNo;
        this.stuName = stuName;
    }

    public Student(int stuNo) {
        this.stuNo = stuNo;
    }

    @Override
    public int compareTo(Student student) {
        int thisNo = this.stuNo;
        int anotherNo = student.stuNo;
        return (thisNo < anotherNo ? -1 : (thisNo == anotherNo ? 0 : 1));
    }

    public String toString() {
        return "这是一个Student类，其中学号为：" + stuNo + "，姓名为：" + stuName;
    }

}

```
