[题目链接](https://codeforces.com/problemset/problem/1844/C)

<br>**提示 1：** 仔细模拟一下，每次操作后不改变什么？
<br>**提示 2：** 最后能“融合”在一起的数字满足什么位置关系？

<br>操作相当于把a[i]+=a[i+2],然后把 a[i+1］和 a[i+2]都去掉。
<br>例如 a=[1,2,3,4,5],去掉 3，把 4 加到 2 中，数组变成[1,6,5]。
<br>注意到5的下标的奇偶性是不变的。
<br>
<br>一般地，由于每次操作都去掉了两个数，**所以操作不会改变剩余元素的下标的奇偶性**。
<br>如果在[1,6,5]的基础上，去掉6，把5加到1中，那么相当于把原数组的 2，3，4 都去掉，把5加到1中。
<br>
<br>一般地，参与求和运算的元素，本质是 a 的子序列，且子序列**相邻元素在 a 中的下标之差都是偶数**。
<br>也就是说，子序列的所有元素的下标，要么都是偶数，要么都是奇数。
<br>
<br>贪心地想，我们可以从 a中偶数下标中选出所有的正数a[1]再求和，记作s0；或者从奇数下标中选出所有的正数a[1]再求和,记作s1。
<br>答案为max(s0,s1)特殊情况：如果所有 a[i]都是负数，那么答案为 max(a)。

python做法如下——
```python 
def solve():
    n = int(input()) 
    a = list(map(int, input().split()))  
    if n == 1:
        print(a[0])
        return
    ji = 0  
    ou = 0 
    j = False 
    o = False 

    for i in range(n):
        if i % 2 == 1:
            if a[i] >= 0:
                ji += a[i]
                j = True
        else: 
            if a[i] >= 0:
                ou += a[i]
                o = True
    ans = max(a) 
    if ji:
        ans = max(ans, ji)
    if ou:
        ans = max(ans, ou)
    print(ans)
    return
```
c++做法如下——
```c++
void solve(){
    int n;
    cin >> n;
    vector<int>a(n);
    for(int i = 0; i < n; i++){
        cin >> a[i];
    }
    if(n == 1){
        cout << a[0] << endl;
        return;
    }
    ll ji = 0;
    ll ou = 0;
    bool j = false;
    bool o = false;
 
    for(int i = 0; i < n; i++){
        if(i % 2){
            if(a[i] >= 0){
                ji += a[i];
                j = true;
            }
 
        }
        else{
            if(a[i] >= 0){
                ou += a[i];
                o = true;
            }
        }
    }
    ll ans = *max_element(a.begin(), a.end());
    if(ji)
    ans = max(ans, ji);
    if(ou)
    ans = max(ans, ou);
    cout << ans << endl;
    return;
}
```
