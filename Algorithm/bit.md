\393. UTF-8 Validation

A character in UTF8 can be from **1 to 4 bytes** long, subjected to the following rules:

1. For 1-byte character, the first bit is a 0, followed by its unicode code.
2. For n-bytes character, the first n-bits are all one's, the n+1 bit is 0, followed by n-1 bytes with most significant 2 bits being 10.

```java
class Solution {
    public boolean validUtf8(int[] data) {
        if (data == null || data.length == 0) {
            return true;
        }
        
        int numOfByte = 0;
        for (int i = 0; i < data.length; ++i) {
            int cur = data[i];
            if (numOfByte == 0) {
                for (int j = 7; j >= 0; --j){
                    if (((1 << j) & cur) == 0) {
                        break;
                    }
                    numOfByte++;
                }
                if (numOfByte == 1 || numOfByte > 4) {
                    return false;
                }
                numOfByte = Math.max(numOfByte, 1);
                
            } else if ((data[i] & 128) != 128) {
                return false;
            }
            numOfByte--;
        }
        return numOfByte == 0;
    }
}
```

