---
layout: post
title: 【莫名其妙】1014 福尔摩斯的约会 (20分) 题解
date: 2020-02-01
author: H_On
description: 垃圾题根本没法做
tag: 题解
---

题目链接：[1014 福尔摩斯的约会 (20分)](https://pintia.cn/problem-sets/994805260223102976/problems/994805308755394560)

### 题目
大侦探福尔摩斯接到一张奇怪的字条：`我们约会吧！ 3485djDkxh4hhGE 2984akDfkkkkggEdsb s&hgsfdk d&Hyscvnm`。大侦探很快就明白了，字条上奇怪的乱码实际上就是约会的时间`星期四 14:04`，因为前面两字符串中第 1 对相同的大写英文字母（大小写有区分）是第 4 个字母 `D`，代表星期四；第 2 对相同的字符是 `E` ，那是第 5 个英文字母，代表一天里的第 14 个钟头（于是一天的 0 点到 23 点由数字 0 到 9、以及大写字母 `A` 到 `N` 表示）；后面两字符串第 1 对相同的英文字母 `s` 出现在第 4 个位置（从 0 开始计数）上，代表第 4 分钟。现给定两对字符串，请帮助福尔摩斯解码得到约会的时间。

### 输入
输入在 4 行中分别给出 4 个非空、不包含空格、且长度不超过 60 的字符串。

### 输出
在一行中输出约会的时间，格式为 `DAY HH:MM`，其中 `DAY` 是某星期的 3 字符缩写，即 `MON` 表示星期一，`TUE` 表示星期二，`WED` 表示星期三，`THU` 表示星期四，`FRI` 表示星期五，`SAT` 表示星期六，`SUN` 表示星期日。题目输入保证每个测试存在唯一解。

### 样例输入
```
3485djDkxh4hhGE
2984akDfkkkkggEdsb
s&hgsfdk
d&Hyscvnm
```

### 样例输出
```
THU 14:04
```

### 解题思路
偷懒使用了 map 容器，很方便的将星期和小时那里的数字对应起来。<br>
* 首先使用前两个字符串，第一个匹配的 **大写字母** 而且一定要是 A-N 中间的一个大写字母来确定星期
* 从第一个匹配到的大写字母 **后面** 开始匹配下一个相同的字母，范围是 0-9 A-N 中的一个字符
* 最后从后两个字符中匹配相同字符，匹配的字符是 a-z A-Z 【这里我就要说话了↓

什么垃圾题？？？什么辣鸡题？？？什么拉几题？？？什么拉吉题？？？什么腊鸡题？？？什么拉机题？？？<br>
各位请看代码最后一块，注释掉了一个 `break;` 我就不明白了，为什么分钟要获取好多个？？？加了break疯狂wa【举报，就是text 4】，去网上搜代码发现思路完全一样，对了半天发现break去掉居然过了，我心情很难受，没了，这道题很简单，我就是想吐槽一下。

顺便，把 **最后不能加 break** 这个坑拿出来给网络增加一个博客也是为了能更容易解救那些陷入这道sha题的无辜少年少女们

### 代码
```c++
#include <iostream>
#include <map>

using namespace std;

int main() {
        ios::sync_with_stdio(0);
        cin.tie(0);
        map<char, string> D, H;

        D['A'] = "MON";
        D['B'] = "TUE";
        D['C'] = "WED";
        D['D'] = "THU";
        D['E'] = "FRI";
        D['F'] = "SAT";
        D['G'] = "SUN";

        H['0'] = "00";
        H['1'] = "01";
        H['2'] = "02";
        H['3'] = "03";
        H['4'] = "04";
        H['5'] = "05";
        H['6'] = "06";
        H['7'] = "07";
        H['8'] = "08";
        H['9'] = "09";
        H['A'] = "10";
        H['B'] = "11";
        H['C'] = "12";
        H['D'] = "13";
        H['E'] = "14";
        H['F'] = "15";
        H['G'] = "16";
        H['H'] = "17";
        H['I'] = "18";
        H['J'] = "19";
        H['K'] = "20";
        H['L'] = "21";
        H['M'] = "22";
        H['N'] = "23";

        string s1, s2; cin >> s1 >> s2;
        int l = min(s1.size(), s2.size()), f = 0;
        for (int i = 0; i < l; i++) {
                if (f == 0 && D.find(s1[i]) != D.end() && s1[i] == s2[i]) cout << D[s1[i]] << ' ', f = 1;
                else if (f == 1 && H.find(s1[i]) != H.end() && s1[i] == s2[i]) cout << H[s1[i]] << ':', f = 2;
                else if (f == 2) break;
        }
        cin >> s1 >> s2;
        l = min(s1.size(), s2.size());
        for (int i = 0; i < l; i++) if (((s1[i] >= 'a' && s1[i] <= 'z') || (s1[i] >= 'A' && s1[i] <= 'Z')) && s1[i] == s2[i]) {
                if (i < 10) cout << '0';
                cout << i << endl;
                //break;
        }
        return 0;
}
```
