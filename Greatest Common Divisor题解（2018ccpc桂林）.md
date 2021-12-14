https://vjudge.net/problem/Gym-102823G
![在这里插入图片描述](https://img-blog.csdnimg.cn/66b2cbfe68664690927d8cecd9599efb.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAUVFRUTIzMg==,size_20,color_FFFFFF,t_70,g_se,x_16)![在这里插入图片描述](https://img-blog.csdnimg.cn/8829fb005d944068a66886a51bf53c4d.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAUVFRUTIzMg==,size_20,color_FFFFFF,t_70,g_se,x_16)
# 题意
给定一个长度为n的整型数组，每次操作给数组中每个值加上1，求最少多少次操作后可以他们的gcd不为1。
# 分析
一个有序数组的gcd为g，则这个有序数组中每一对相邻的数组的差的gcd必含有因子g
证明如下：

 1. 设数组{a，b，c}的gcd为g；
 2. 令a = a~1~g，b = a~2~g，c = a~3~g；
 3. 则b - a = （a~2~ -  a~1~ ）g ，c - b = （a~3~ - a~2~）g
 4. 则（b - a）于 （c - b）含有共同因子g
 5. 由此推得：一个数组{a~1~，a~2~，a~3~，……，a~n~}gcd为g
 6. 则{a~2~ - a~1~，a~3~ - a~2~，……，a~n~ - a~n-1~}的gcd含有因子g


由此可得，若进行+1操作后的数组的gcd一定是他们相邻的差的gcd的因子之一。而他们相邻的差是不会因为他们的进行多少次+1操作而改变。所以我们可以先求原数组相邻的差的gcd再将这个gcd唯一分解，找出那个符合题目条件的因子。
# AC代码
```cpp
#include <bits/stdc++.h>

using namespace std;

long long a[100005];

long long solve(int);

int main()
{
    int n;
    scanf("%d", &n);
    for (int i = 1; i <= n; i++)
        printf("%lld\n", solve(i));
    return 0;
}

long long solve(int qqq)
{
    int n;
    cin >> n;
    for (int i = 1; i <= n; i++)
        scanf("%lld", &a[i]);
    sort(a + 1, a + 1 + n);//排序变成有序数组
    cout << "Case " << qqq << ": ";
    long long gcd = -1;
    for (int i = 2; i <= n; i++)
    {
        long long d = a[i] - a[i - 1];
        if (!d)
            continue;
        if (gcd == -1)
            gcd = d;
        else
            gcd = __gcd(gcd, d);
    }
    if (gcd == -1 && a[1] != 1)//若全部相等并且值不为1则不需要+1
        return 0;
    if (gcd == -1 && a[1] == 1)//若全部相等并且值为1，则只要+1即可
        return 1;
    if (gcd == 1)//若gcd为1，则不论多少次+1都无法得到符合题目条件的数组
        return -1;
    long long gcds = gcd;
    vector<long long> f;
    for (long long i = 2; i * i <= gcd; i++)
    {
    	//唯一分解
        if (gcd % i == 0)
        {
            f.push_back(i);
            while (gcd % i == 0)
                gcd /= i;
        }
    }
    if (gcd > 1)
        f.push_back(gcd);
    long long ans = 1e18;
    for(auto i : f)
    {
        if(a[1] % i == 0) ans = 0;
        ans = min (ans, i - (a[1] % i));
    }
    return ans;
}
```

