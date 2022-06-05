1022 D进制的A+B (20 point(s))

## 1 题目

输入两个非负 10 进制整数 *A* 和 *B* (≤230−1)，输出 *A*+*B* 的 *D* (1<*D*≤10)进制数。

### 输入格式：

输入在一行中依次给出 3 个整数 *A*、*B* 和 *D*。

### 输出格式：

输出 *A*+*B* 的 *D* 进制数。

### 输入样例：

```in
123 456 8
```

### 输出样例：

```out
1103
```

## 2 解答：

思路：10进制转换成X进制，利用除法取余数实现，申请一个数组来存放余数，最后遍历数组，输出转换后的进制

### C++：

```cpp
#include<iostream>
using namespace std;

int main()
{
    int A, B, D;
    cin >> A >> B >> D;
    int sum;
    sum = A + B; // 两数相加
    int arr[32] = { 0 }; // 申请数组存放余数
    int i = 0;
    while(sum != 0) {
        arr[i] = sum % D;
        sum = sum / D;
        i++;
    }
    if(i == 0) { // 如果两数之和为0，输出0
        cout << arr[0];
    }
    else { // 遍历数组，输出转换后的进制
        for(i--;i>=0;i--) {
            cout << arr[i];
        }
    }
     cout << endl; 
    
}
```