1036 Boys vs Girls (25 point(s))

## 1 题目

This time you are asked to tell the difference between the lowest grade of all the male students and the highest grade of all the female students.

### Input Specification:

Each input file contains one test case. Each case contains a positive integer *N*, followed by *N* lines of student information. Each line contains a student's `name`, `gender`, `ID` and `grade`, separated by a space, where `name` and `ID` are strings of no more than 10 characters with no space, `gender` is either `F` (female) or `M` (male), and `grade` is an integer between 0 and 100. It is guaranteed that all the grades are distinct.

### Output Specification:

For each test case, output in 3 lines. The first line gives the name and ID of the female student with the highest grade, and the second line gives that of the male student with the lowest grade. The third line gives the difference *g**r**a**d**e**F*−*g**r**a**d**e**M*. If one such kind of student is missing, output `Absent` in the corresponding line, and output `NA` in the third line instead.

### Sample Input 1:

```in
3
Joe M Math990112 89
Mike M CS991301 100
Mary F EE990830 95
```

### Sample Output 1:

```out
Mary EE990830
Joe Math990112
6
```

### Sample Input 2:

```in
1
Jean M AA980920 60
```

### Sample Output 2:

```out
Absent
Jean AA980920
NA
```

## 2 解答

### C++：

初步想法，还是有多少个同学，就循环多少次，但本题区分性别依次更新即可。最后按要求输出

**要点：**输出时女生第一行先输出，男生第二行输出，且当某个性别为空时，Absent也按此顺序

```cpp
#include<iostream>
using namespace std;
#include<string>

int main()
{
    int N;
    cin >> N;
    string name, gender, id; // 每行输入的同学的信息
    int grade; // 每行输入的同学的信息
    int f_MAX=-1, m_MIN=101; // 临时值用来循环变更
    string m_id, f_id, m_name, f_name; // 输出的同学的值
    
    int count_f = 0, count_m = 0; // 记录男性/女性的人生
    for(int i = 0; i < N; i++)
    {
        cin >> name >> gender >> id >> grade;
        /*更新*/
        if(!gender.compare("M") && grade<m_MIN)
        {
            m_MIN = grade;
            m_id = id;
            m_name = name;
            count_m++;
        }
        if(!gender.compare("F") && grade>f_MAX)
        {
            f_MAX = grade;
            f_id = id;
            f_name = name;
            count_f++;
        }
        /*更新*/
    }
    
    if (count_m == 0 && count_f == 0) // 如果输入为0
    {
        cout << "Absent" << "\n" << "Absent" << "\n" << "NA" << endl;
    }
    else if(count_f == 0) // 如果女同学为0，先输出Absent，再输入男同学
    {
        cout << "Absent" << "\n" << m_name << " "  << m_id << "\n" << "NA" << endl;
    }
    else if(count_m == 0) // 如果男同学为0，先输出女同学，再输出Absent
    {
        cout << f_name << " " << f_id << "\n" << "Absent" << "\n"<< "NA" << endl;
    }
    else // 正常情况 先输出女同学，再输出男同学，再分差
    {
        cout << f_name << " " << f_id << "\n" << m_name << " "  << m_id << "\n" << (f_MAX - m_MIN) << endl;
    }
}
```