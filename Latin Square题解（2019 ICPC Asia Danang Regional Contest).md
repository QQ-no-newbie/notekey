## 标签：二分图




https://vjudge.net/problem/Kattis-latinsquare
这题在说白了就是一道数独，hhhhhhhhh
训练赛的时候根本看不出是一道二分图，甚至根本没往这方面想，结束时看题解也是莫名奇妙（那篇题解没有讲解），到后面问了学长，学长提了一嘴。瞬间顿悟！！！！
首先，这个是一个二分图覆盖的模型每一行每一列只能有一个同一数字。
于是乎我们将他分解成多步，每一步就是将一个种类的数字，填进矩阵。
所以，每一步就是一个最小点覆盖，将第i行和第j列抽象成两个点，i -> j就是一条边，找不同i且不同j进行一个匹配，将所有的i和j匹配完后，就是一个最小点覆盖。
（我自己的理解，讲的不清楚可以看看代码，代码比较好理解）
```cpp
#include <bits/stdc++.h>
using namespace std;
int maps[110][110];
int bj[110], match[110];
bool mark[110];****
int n, k;
int find(int x);
int main()
{
    scanf("%d%d", &n, &k);
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++)
        {
            int x;
            scanf("%d", &x);
            maps[i][j] = x;
            mark[x] = 1;
        }
    for (int i = 1; i <= n; i++)
    {
        if (mark[i])
            continue;
        memset(match, 0, sizeof match);
        for (int j = 1; j <= n; j++)
        {
            memset(bj, 0, sizeof bj);
            find(j);
        }
        for (int j = 1; j <= n; j++)
        {
            maps[match[j]][j] = i;
        }
    }
    cout << "YES\n";
    for (int i = 1; i <= n; i++)
    {
        for (int j = 1; j <= n; j++)
            cout << maps[i][j] << " ";
        cout << endl;
    }
    return 0;
}
int find(int x)
{
    for (int i = 1; i <= n; i++)
    {
        if (!bj[i] && !maps[x][i])
        {
            bj[i] = 1;
            if (!match[i] || find(match[i]))
            {
                match[i] = x;
                return 1;
            }
        }
    }
    return 0;
}
```



