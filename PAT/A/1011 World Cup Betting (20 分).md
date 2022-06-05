1011 World Cup Betting (20 分)

## 1 题目描述

With the 2010 FIFA World Cup running, football fans the world over were becoming increasingly excited as the best players from the best teams doing battles for the World Cup trophy in South Africa. Similarly, football betting fans were putting their money where their mouths were, by laying all manner of World Cup bets.

Chinese Football Lottery provided a "Triple Winning" game. The rule of winning was simple: first select any three of the games. Then for each selected game, bet on one of the three possible results -- namely `W` for win, `T` for tie, and `L` for lose. There was an odd assigned to each result. The winner's odd would be the product of the three odds times 65%.

For example, 3 games' odds are given as the following:

```
 W    T    L
1.1  2.5  1.7
1.2  3.1  1.6
4.1  1.2  1.1
```

To obtain the maximum profit, one must buy `W` for the 3rd game, `T` for the 2nd game, and `T` for the 1st game. If each bet takes 2 yuans, then the maximum profit would be (4.1×3.1×2.5×65%−1)×2=39.31 yuans (accurate up to 2 decimal places).

### Input Specification:

Each input file contains one test case. Each case contains the betting information of 3 games. Each game occupies a line with three distinct odds corresponding to `W`, `T` and `L`.

### Output Specification:

For each test case, print in one line the best bet of each game, and the maximum profit accurate up to 2 decimal places. The characters and the number must be separated by one space.

### Sample Input:

```in
1.1 2.5 1.7
1.2 3.1 1.6
4.1 1.2 1.1
```

### Sample Output:

```out
T T W 39.31
```

## 2 解答

### C++:

因为题目说是输入三个游戏，每行代表一个游戏，且每行三个数值。因此，初步想法就是创建一个3x3的数组来存放输入的数值，同时因为题目所要输入每行数值的最大值对应的字母，所以想法是开创一个存放3个数值（3次游戏）的一维数组来存放每行输入的最大值的位置。

接着，就依次遍历每行找出每行输入的最大值的位置，到最后输出其对应的字母，以及计算最终结果。

```c++
#include<iostream>
using namespace std;
#include<iomanip> // 保留小数 
int main()
{
    float arr[3][3]; // 存放输入数据 
    int max;  // 过渡值 
    int arrmax[3]; // 存放每行最大元素所在的位置 
    /*以下为输入数据*/
    for(int i = 0; i < 3; i++)
    {
        for(int j = 0; j < 3; j++)
        {
            cin >> arr[i][j];
        }
    }
    /*以上为输入数据*/ 
    for(int i = 0; i < 3; i++)
    {
        max = arr[i][0]; // 首先记录每行第一个元素为最大值 
        arrmax[i] = 0; 
        for(int j = 0; j < 3; j++)
        {
            if(arr[i][j] > max) // 遍历每行数组 找出每行元素最大值所在的位置 
            {
                max = arr[i][j];  
                arrmax[i] = j;
            }
        }
    }
    
    float sum = 1;
    for(int i = 0; i < 3; i++)
    {
	    sum = sum  * arr[i][arrmax[i]];
	    /*输出每行元素最大值所属位置的 对应的 字母*/
        if(arrmax[i] == 0) 
		{
            cout << "W" << " ";
		}
        else if(arrmax[i] == 1)
		{
            cout << "T" << " ";
		}
        else 
		{
            cout << "L" << " ";
		}
    }
    
    sum = (sum * 0.65 - 1) * 2;
    cout << fixed << setprecision(2) << sum << endl;  // 保留小数 
}
```