# 基本概念

- s[ ] 模式串

- p[ ] 模板串

- 非平凡前缀 : 指除了最后一个字符以外，一个字符串的全部头部组合。
- 非平凡后缀 : 指除了第一个字符以外，一个字符串的全部尾部组合。（后面会有例子，均简称为前/后缀）
- 部分匹配值 : 前缀和后缀的最长共有元素的长度。

- next[ ] 是 部分匹配值表 ，即next数组，它存储的是每一个下标对应的“部分匹配值”，是KMP算法的核心。（后面作详细讲解）。



# 代码

```c++
#define _CRT_SECURE_NO_WARNINGS
#include<iostream>
#include<cstdio>
#include<cstring>

using namespace std;

const int N = 1e6 + 5;

int ne[N];
char s[N], p[N];
int j;

int main()
{
    scanf("%s%s", s + 1, p + 1);

    int lens = strlen(s + 1), lenp = strlen(p + 1);

    for (int i = 2; i <= lenp; i++)
    {
        while (j && p[j + 1] != p[i])
            j = ne[j];
        if (p[j + 1] == p[i])
            j++;
        ne[i] = j;
    }
    j = 0;
    for (int i = 1; i <= lens; i++)
    {
        while (j && s[i] != p[j + 1])
            j = ne[j];
        if (s[i] == p[j + 1])
            j++;
        if (j == lenp)
            printf("%d\n", i - lenp + 1), j = ne[j];
    }

    for (int i = 1; i <= lenp; i++)
        printf("%d ", ne[i]);

    return 0;
}
```

