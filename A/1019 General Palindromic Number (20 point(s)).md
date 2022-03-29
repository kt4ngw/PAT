1019 General Palindromic Number (20 point(s))

## 1 题目

A number that will be the same when it is written forwards or backwards is known as a **Palindromic Number**. For example, 1234321 is a palindromic number. All single digit numbers are palindromic numbers.

Although palindromic numbers are most often considered in the decimal system, the concept of palindromicity can be applied to the natural numbers in any numeral system. Consider a number *N*>0 in base *b*≥2, where it is written in standard notation with *k*+1 digits *a**i* as ∑*i*=0*k*(*a_**{i}**b**i*). Here, as usual, 0≤*a**i*<*b* for all *i* and *a**k* is non-zero. Then *N* is palindromic if and only if *a**i*=*a**k*−*i* for all *i*. Zero is written 0 in any base and is also palindromic by definition.

Given any positive decimal integer *N* and a base *b*, you are supposed to tell if *N* is a palindromic number in base *b*.

### Input Specification:

Each input file contains one test case. Each case consists of two positive numbers *N* and *b*, where 0<*N*≤109 is the decimal number and 2≤*b*≤109 is the base. The numbers are separated by a space.

### Output Specification:

For each test case, first print in one line `Yes` if *N* is a palindromic number in base *b*, or `No` if not. Then in the next line, print *N* as the number in base *b* in the form "*a**k* *a**k*−1 ... *a*0". Notice that there must be no extra space at the end of output.

### Sample Input 1:

```in
27 2
```

### Sample Output 1:

```out
Yes
1 1 0 1 1
```

### Sample Input 2:

```in
121 5
```

### Sample Output 2:

```out
No
4 4 1
```

## 2 解答

思路：本文是将输入的数N，转换成b进制的数，然后判断这个b进制的数是否为回文数。

首先将输入的数转换成对应的进制（利用数组存放），然后双指针分别从前从后遍历该数组，判断是否为回文数。

### C++：

```cpp
#include<iostream>
using namespace std;

int main()
{
    int N, b;
    cin >> N >> b;
    /*转换进制，并将结果存放到数组中*/
    int arr[32] = { 0 };
    int i = 0;
    while(N != 0)
    {
        arr[i] = N % b;
        N = N / b;
        i++;
    }
    /*转换进制，并将结果存放到数组中*/
    int flag = 1; // 最初都标记为回文
    int end = i-1, first = 0;
    for(;first <= (end - first)/2;end--,first++) // 双指针分别从前从后遍历该数组
    {
        if(arr[first] != arr[end]) // 判断是否为回文数
        {
            flag = 0;
            break;
        }
    }
    if(flag == 1)
    {
        cout << "Yes" << "\n";
    }
    else{
        cout << "No" << "\n";
    }
    int k = i - 1;
    for(; k > 0; k--) // 输入进制转换后的数
    {
        cout << arr[k] << " ";
    }
    cout << arr[k] << endl;
}
```