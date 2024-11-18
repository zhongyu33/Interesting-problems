[题目链接](https://codeforces.com/problemset/problem/610/C)
<br>**提示 1：** 比较纯粹的构造题。可以先尝试较小的 $k$ 。

**提示 2：** 从 $k$ 到 $k+1$ ，整体相当于是四个 $2^k\times 2^k$ 的正方形，有没有办法利用前一次的构造结果构造下一个？

<br>本题的一种发现答案的方法是直接手动构造 $k=1,2,3,\dots$ 的情况，找规律以生成最终矩阵，但这个有时候得看做题的状态和灵性。
<br>我们考虑用递推构造的方法。
<br>我们发现从 $k$ 到 $k+1$ 时，相当于从 $2^k\times 2^k$ 的矩阵变成了 $2^{k+1}\times 2^{k+1}$ 的矩阵，我们把后者上下左右拆开，可以拆成 $2\times 2$ 个 $2^k\times 2^k$ 的矩阵。
<br>假设我们已经完成了 $2^k\times 2^k$ 的矩阵 $A$ ，怎么进一步构造新的大矩阵呢？
<br> $k$ :
<br> *
<br> $k+1$:
<br>**
<br>*+
<br> $k+2$:
<br>****
<br>*+*+
<br>**++
<br>*++*
<br>可以发现，一二三象限不变，4象限取反即可。

Python 做法如下——

```Python []
def change(cur):
    ans = []
    for i in cur:
        if i == '*':
            ans.append("+")
        else:
            ans.append("*")
    return ans
def dfs(i):
    if i == 0:
        return [['+']]
    last = dfs(i - 1)
    ans = []
    for i in last:
        ans.append(i + i)
    for i in last:
        ans.append(i + change(i))
    return ans
def solve():
    ans = dfs(int(input()))
    for i in ans:
        print("".join(i))
```
C++ 做法如下——

```cpp []
vector<char> change(const vector<char> &cur){
    vector<char>ans;
    for(auto i : cur){
        if (i == '*'){
            ans.push_back('+');
        }
        else{
            ans.push_back('*');
        }
    }
    return ans;
}

vector<vector<char>> dfs(int i){
    vector<vector<char>>ans;
    if(i == 0){
        return {{'+'}};
    }
    vector<vector<char>> last = dfs(i - 1);
    for(auto j : last){
        vector<char>mid = j;
        mid.insert(mid.end(), j.begin(), j.end());
        ans.push_back(mid);
    }
    for(auto j : last){
        vector<char>mid = j;
        j = change(j);
        mid.insert(mid.end(), j.begin(), j.end());
        ans.push_back(mid);
    }
    return ans;
}
void solve() {
    int n;
    cin >> n;
    vector<vector<char>>ans;
    ans = dfs(n);
    for(auto i : ans){
        for(auto j : i){
            cout << j;
        }
        cout << endl;
    }
    return;
}
```
