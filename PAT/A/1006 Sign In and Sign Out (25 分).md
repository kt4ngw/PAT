1006 Sign In and Sign Out (25 分)

## 1 题目

At the beginning of every day, the first person who signs in the computer room will unlock the door, and the last one who signs out will lock the door. Given the records of signing in's and out's, you are supposed to find the ones who have unlocked and locked the door on that day.

### Input Specification:

Each input file contains one test case. Each case contains the records for one day. The case starts with a positive integer *M*, which is the total number of records, followed by *M* lines, each in the format:

```
ID_number Sign_in_time Sign_out_time
```

where times are given in the format `HH:MM:SS`, and `ID_number` is a string with no more than 15 characters.

### Output Specification:

For each test case, output in one line the ID numbers of the persons who have unlocked and locked the door on that day. The two ID numbers must be separated by one space.

Note: It is guaranteed that the records are consistent. That is, the sign in time must be earlier than the sign out time for each person, and there are no two persons sign in or out at the same moment.

### Sample Input:

```in
3
CS301111 15:30:28 17:00:10
SC3021234 08:00:00 11:25:25
CS301133 21:45:00 21:58:40
```

### Sample Output:

```out
SC3021234 CS301133
```

## 2 解答

### C++：

找出M个人中谁先进实验室，谁最后出实验室。

本文想法就是先设定一个界限值，然后一个个输入比较，如果循环中同学的时间早于上一位同学来实验室的时间，则交换变量；同理循环中同学的时间晚于上一位同学来实验室的时间，则交换变量。循环结束后，就输入记录的id即可。

时间变量可ASCII码直接比较出结果

```cpp
#include<iostream>
using namespace std;

int main()
{
    int M;
    cin >> M;
    string id, in, out;
    string e_id, l_id;
    string e_time = "23:59:59", l_time = "00:00:00"; // 先设定边界时间
    for(int i = 0; i < M; i++) // M个人输入
    {
        cin >> id >> in >> out;
        if(in < e_time) // 如果这同学的时间早于上一位同学来实验室的时间
        {               // 则交换输出id，且换一下e_time
            e_id = id;
            e_time = in;
        }
        if(out > l_time) // 如果这同学的时间晚于上一位同学来实验室的时间
        {                // 则交换输出id，且换一下l_time          
            l_id = id;
            l_time = out;
        }
    }
    cout << e_id << " " << l_id << endl;
    return 0;
}
```