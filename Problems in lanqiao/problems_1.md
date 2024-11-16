**题目**：输入n(1<=n<=1e5)和长度为n的数组a(1<=a[i]<=1e9)，每次操作你可以选择一个下标，使得该下标元素值不变，其余所有元素值加一。问最少操作几次可以使数组a中所有元素都相等？
<br>输入样例:
<br>3
<br>2 2 3
<br>输出样例:
<br>1

<br>**提示1**：其余元素都加一等价于什么？
<br>**提示2**：目标值为几？

<br>一道普通的脑筋急转弯
<br>以被选中的数字的视角来看，该下标元素值不变，其余所有元素值加一，但是以其余元素的视角来看呢，就是其余元素值不变，该元素值减1，这样，问题就变成了每次操作你可以选择一个下标，使得该下标元素值减少一，问最少操作几次可以使数组a中所有元素都相等，答案显而易见用最小值为目标值，遍历数组累加差值即可
<br>
<br>python代码如下————:
```python 
def solve():
    n = int(input())
    a = list(map(int, input().split()))
    ans = 0
    m = min(a)
    for i in a:
        ans += i - m
    print(ans)
```
<br>c++代码如下————:
```c++
void solve() {
    int n;
    cin >> n;
    vector<int>a(n);
    for(int i = 0; i < n; i++){
        cin >> a[i];
    }
    int m = *min_element(a.begin(), a.end());
    int ans = 0;
    for(int i : a){
        ans += i - m;
    }
    cout << ans << endl;
    return;
}
```
