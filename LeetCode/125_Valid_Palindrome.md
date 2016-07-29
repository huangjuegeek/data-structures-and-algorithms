## 125. Valid Palindrome
> https://leetcode.com/problems/valid-palindrome/

#### Solution 1:
> https://discuss.leetcode.com/topic/5581/here-s-a-clean-c-solution/2

```cpp
class Solution {
public:
    bool isPalindrome(string s) {
        for (int i = 0, j = s.size() - 1; i < j; i++, j--) { // Move 2 pointers from each end until they collide
            while (!isalnum(s[i]) && i < j) i++; // Increment left pointer if not alphanumeric
            while (!isalnum(s[j]) && i < j) j--; // Decrement right pointer if no alphanumeric
            if (toupper(s[i]) != toupper(s[j])) return false; // Exit and return error if not match
        }
        return true;
    }
};
```

```java
public class Solution {
	public boolean isPalindrome(String s) {
		if (s == null || s.length() == 0) {
			return true;
		}

		s = s.trim();

		int i = 0;
		int j = s.length() - 1;

		while (i < j) {
			char c1 = s.charAt(i);
			char c2 = s.charAt(j);
			if (!Character.isLetterOrDigit(c1)) {
				i++;
				continue;
			}
			if (!Character.isLetterOrDigit(c2)) {
				j--;
				continue;
			}
			if (!isSame(c1, c2)) {
				return false;
			} else {
				i++;
				j--;
			}
		}
		return true;
	}

	private boolean isSame(char c1, char c2) {
		if ((c1 >= '0' && c1 <= '9') || (c2 >= '0' && c2 <= '9')){
	        return c1 == c2;
	    } else {
	        return c1 == c2 || Math.abs(c1 - c2) == 'a' - 'A';
	    }
	}
}
```
