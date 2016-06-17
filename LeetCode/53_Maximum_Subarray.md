## Maximum Subarray
> https://leetcode.com/problems/maximum-subarray/

#### Solution 1: Dynamic Programming, time O(N)
http://blog.csdn.net/linhuanmars/article/details/21314059
```java
// without extra array
public class Solution {
	public int maxSubArray(int[] A) {
		if (A == null || A.length == 0)
			return 0;
		int global = A[0];
		int local = A[0];
		for (int i = 1; i < A.length; i++) {
			local = Math.max(A[i], local + A[i]);
			global = Math.max(local, global);
		}
		return global;
	}
}
```
```java
/// with extra array
public class Solution {
	public int maxSubArray(int[] A) {
		int global = A[0];
		int[] local = new int[A.length];
		local[0] = A[0];

		for (int i = 1; i < A.length; i++) {
			local[i] = Math.max(A[i], local[i - 1] + A[i]);
			global = Math.max(global, local[i]);
		}

		return global;
	}
}
```
#### Solution 2: Divide and Conquer
http://www.cnblogs.com/springfor/p/3877058.html
```java
public class Solution {
	public int maxSubArray(int[] A) {
		return divide(A, 0, A.length - 1);
	}

	public int divide(int A[], int low, int high) {
		if (low == high)
			return A[low];
		if (low == high - 1)
			return Math.max(A[low] + A[high], Math.max(A[low], A[high]));

		int mid = (low + high) / 2;
		int lmax = divide(A, low, mid - 1);
		int rmax = divide(A, mid + 1, high);

		int mmax = A[mid];
		int tmp = mmax;
		for (int i = mid - 1; i >= low; i--) {
			tmp += A[i];
			if (tmp > mmax)
				mmax = tmp;
		}
		tmp = mmax;
		for (int i = mid + 1; i <= high; i++) {
			tmp += A[i];
			if (tmp > mmax)
				mmax = tmp;
		}
		return Math.max(mmax, Math.max(lmax, rmax));

	}
}
```
