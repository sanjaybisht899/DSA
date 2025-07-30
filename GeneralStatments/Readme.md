1. The test cases are generated so that the answer fits in a 32-bit integer.

Any value that your program returns (such as the length or indices of the longest palindromic substring) will not exceed the maximum value of a 32-bit signed integer, which is:

2^31 -1 = 2,147,483,647

So if your solution uses integer variables like int start, int end, or int length, you don't need to worry about integer overflow,

You can safely use: int start = 0; int maxLen = 0;
No need for: long start = 0L;  // Not needed


2. 