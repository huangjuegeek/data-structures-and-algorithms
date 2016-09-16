* Greatest Common Divisor (GCD)
```java
public class Main {
    //最大公约数
    static int gcd(int num1, int num2) {
        while(num2 != 0) {
            int temp = num2;
            num2 = num1 % num2;
            num1 = temp;
        }
        return num1;
    }

    public static void main(String[] args) {
        System.out.println(gcd(36, 24));
        System.out.println(gcd(24, 36));
        System.out.println(gcd(24, 32));
        System.out.println(gcd(32, 24));
        System.out.println(gcd(16, 32));
        System.out.println(gcd(32, 16));
    }
}
```
