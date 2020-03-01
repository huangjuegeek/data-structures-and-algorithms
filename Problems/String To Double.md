将字符串转成double
```java
public class StringToDouble {

    public static double convert(String str) {
        if (str == null || str.isEmpty()) {
            throw new IllegalArgumentException("str is null or empty!");
        }

        boolean isNegative = false;
        int len = str.length();

        char first = str.charAt(0);
        int i = 0;
        if (first == '+' || first == '-') {
            if (len == 1) {
                throw new IllegalArgumentException(str);
            }
            if (first == '-') {
                isNegative = true;
            }
            i++;
        } else if (!Character.isDigit(first)) {
            throw new IllegalArgumentException(str);
        }

        String[] strArr = str.split("\\.");
        if (strArr.length > 2) {
            throw new IllegalArgumentException(str);
        }

        String left = strArr[0];
        int leftLen = left.length();

        double leftRes = 0.0;
        int cur;

        for (; i < leftLen; i++) {
            if (!Character.isDigit(left.charAt(i))) {
                throw new IllegalArgumentException(str);
            }
            cur = left.charAt(i) - '0';
            leftRes = leftRes * 10 + cur;
        }

        if (strArr.length == 2) {
            String right = strArr[1];
            int rightLen = right.length();
            double rightRes = 0.0;
            for (i = 0; i < rightLen; i++) {
                if (!Character.isDigit(right.charAt(i))) {
                    throw new IllegalArgumentException(str);
                }
                cur = right.charAt(i) - '0';
                rightRes += cur / Math.pow(10, i+1);
            }
            leftRes += rightRes;
        }

        return isNegative ? -leftRes : leftRes;
    }

    public static void test(String str) {
        System.out.println("==================================");
        System.out.println("str->   " + str);
        try {
            System.out.println("double->" + convert(str));
        } catch (Exception e) {
            System.out.println("IllegalArgumentException: " + str);
        }
    }

    public static void main(String[] args) {
        test("+2.");
        test("0");
        test("0.0");
        test("24124124");
        test("+2.0");
        test("-2.999");
        test("fsd13r");
        test(".21897498124");
        test("0.124798124");
        test("9..9");
        test("3423.42354.1313");
        test("55555555555555555555555555555555555555");
        test("6.88888888888888888888888888888888888888888888888");
        test("7777777777777777777777777777777777777777.4444444444444444444444444444444444444444444444444444");

        System.out.println();
    }
}

```
