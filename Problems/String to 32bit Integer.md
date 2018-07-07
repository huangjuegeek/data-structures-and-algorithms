```java
/*
把一个给定字符串转成32位整数
 */
public class StringTo32Int {

    public static int convertStringToInt(String str) {
        if (str == null || str.isEmpty()) {
            throw new IllegalArgumentException("null or empty");
        }
        
        boolean isNegative = false;
        int i = 0;
        int len = str.length();

        char first = str.charAt(0);
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

        int res = 0;
        int cur = 0;
        int minDiv = Integer.MIN_VALUE / 10;
        int minMod = Integer.MIN_VALUE % 10;

        for (; i < len; i++) {
            if (!Character.isDigit(str.charAt(i))) {
                throw new IllegalArgumentException(str);
            }
            cur = '0' - str.charAt(i);
            if ((res < minDiv) || (res == minDiv && cur < minMod)) {
                throw new IllegalArgumentException(str);
            }
            res = res * 10 + cur;
        }
        
        if (!isNegative && res == Integer.MIN_VALUE) {
            throw new IllegalArgumentException(str);
        }
        
        return isNegative ? res : -res;
    }
    
    public static void main(String[] args) {
        String str = null;
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "+";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "-";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "++";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "--";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "+0";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "-0";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "+adf";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "xyz";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "+123";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "-123";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "123";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "2147483647";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "2147483648";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }

        str = "-2147483648";
        try {
            System.out.println(str + " -> " + convertStringToInt(str));
        } catch (IllegalArgumentException e) {
            e.printStackTrace();
        }
    }
}
```
