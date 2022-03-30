1027 Colors in Mars (20 point(s))

## 1 题目	

People in Mars represent the colors in their computers in a similar way as the Earth people. That is, a color is represented by a 6-digit number, where the first 2 digits are for `Red`, the middle 2 digits for `Green`, and the last 2 digits for `Blue`. The only difference is that they use radix 13 (0-9 and A-C) instead of 16. Now given a color in three decimal numbers (each between 0 and 168), you are supposed to output their Mars RGB values.

### Input Specification:

Each input file contains one test case which occupies a line containing the three decimal color values.

### Output Specification:

For each test case you should output the Mars RGB value in the following format: first output `#`, then followed by a 6-digit number where all the English characters must be upper-cased. If a single color is only 1-digit long, you must print a `0` to its left.

### Sample Input:

```in
15 43 71
```

### Sample Output:

```out
#123456
```



## 2 解答

思路：题目是说将输入的三个10进制的数转换成13进制，因为13进制存在ABC，故开辟一个数组来存放。又168<13**2，所以两位13进制数就可以表示输入的10进制数。

由题意说，如果输入的10进制是 0 43 71 输出也要是 #003456.（ you must print a `0` to its left.） 

故输入一个10进制数将其整除的商就为13进制的第一位，余数就为第二位。

### C++：

```cpp
#include<iostream>
using namespace std;

int main()
{
    char str[13] = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C'}; 
    int Red, Green, Blue;
    cin >> Red >> Green >> Blue;
    cout << "#" << str[Red/13] << str[Red%13] << str[Green/13] << str[Green%13] << str[Blue/13] << str[Blue%13] << endl;
}
    
```

