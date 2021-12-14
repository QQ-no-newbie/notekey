# QQ打cf

http://120.78.128.11/Problem.jsp?pid=4364

这题就是一道简单的签到，题目要我们删除最大位数的数，简单来说就是如果一个数字串中有合数或者1那么就可以删到只剩下那个合数（或者1）就好了。（看不懂直接看代码把）
```cpp
#include <bits/stdc++.h>
using namespace std;
char a[100];
int main()
{
    int t;
    cin >> t;
    while (t--)
    {
        int n;
        scanf("%d", &n);
        scanf("%s", a + 1);
        if (n == 1)
        {
            printf("1\n");
            continue;
        }
        bool flag = 0;
        for (int i = 1; i <= n; i++)
        {
            if (a[i] != '2' && a[i] != '3' && a[i] != '5' && a[i] != '7')
            {
                printf("1\n");
                flag = 1;
                break;
            }
        }
        if (flag)
            continue; 
        printf("2\n");
    }
    return 0;
}
```
