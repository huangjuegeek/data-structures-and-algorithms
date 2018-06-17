# 计算(x^y)%N
```java
import java.math.BigInteger;

public class XpowYmodN {

    public static void main(String[] args) {
        XpowYmodN solution = new XpowYmodN();

        long max = 10;
        for (long x = 1; x <= max ; x++) {
            for (long y = 1; y <= max; y++) {
                for (long N = 1; N <= max; N++) {
                    System.out.printf("x=%d, y=%d, N=%d\n", x, y , N);
                    System.out.println("xPowYmodN result: " + solution.xPowYmodN(x, y, N));
                    System.out.println("xPowYmodN1 result: " + solution.xPowYmodN1(x, y, N));
                    System.out.println("xPowYmodN2 result: " + solution.xPowYmodN2(x, y, N));
                }
            }
        }
    }

    /**
     * (x^y)%N   x的y次方 对N取模
     * @param x
     * @param y
     * @param N
     * @return
     */
    public long xPowYmodN(long x, long y, long N) {
        long res = 1;
        x = x % N;

        while (y > 0) {
            if (y % 2 == 1) {
                res = (res * x) % N;
            }
            y /= 2;
            x = (x * x) % N;
        }

        return res;
    }

    public long xPowYmodN1(long x, long y, long N) {
        BigInteger bX = BigInteger.valueOf(x);
        BigInteger bY = BigInteger.valueOf(y);
        BigInteger bN = BigInteger.valueOf(N);

        BigInteger res = bX.modPow(bY, bN);
        return res.longValue();
    }

    public long xPowYmodN2(long x, long y, long N) {
        double in = Math.pow(x, y);
        long res = (long)(in % N);
        return res;
    }
}

```
