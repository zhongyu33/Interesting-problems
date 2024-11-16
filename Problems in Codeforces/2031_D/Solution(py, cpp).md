**提示1** 答案是否满足某种单调性？
<br>**提示2** 答案的最后一个值可以很容易确定，那么怎么向前递推呢？
<br>可以容易想到，答案一定是单调不减的，而且最后一个数字一定为max(nums)
<br>用pre数组存前缀最大值，suf存后缀最小值。接下来如对于下标i的数字，我们尽量让他等于i+1就行。
我们发现，当pre[i]大于suf[i + 1]时，i号位置一定可以先跳到值等于pre[i]的位置, 在跳到值等于suf[i + 1]的位置，
<br>这样i下标的值就等于值为suf[i + 1]的位置的值，由于其单调性，因此ans[i] = ans[i + 1].
反之，如果pre[i] <= suf[i + 1]，该位置就无法“后跳”，所以ans[i] = pre[i]


python做法如下——
```python 
def solve():
    n = int(input())
    a = list(map(int, input().split()))
    pre = a[:]
    for i in range(1, n):
        pre[i] = max(pre[i], pre[i - 1])
    suf = a[:]
    for i in range(n - 2, -1, -1):
        suf[i] = min(suf[i], suf[i + 1])
    a[-1] = pre[-1]
    for i in range(n - 2, -1, -1):
        if pre[i] > suf[i + 1]:
            a[i] = a[i + 1]
        else:
            a[i] = pre[i]
    print(*a)
```
c++做法如下——
```c++
void solve() {
    int n;
    cin >> n;
    vector<int>a(n), suf(n), pre(n);
    
    for(int i = 0; i < n; i++){
        cin >> a[i];
        suf[i] = a[i];
        pre[i] = a[i];
    }
    for(int i = 1; i < n; i++){
        pre[i] = max(pre[i], pre[i - 1]);
    }
    for(int i = n - 2; i > -1; i--){
        suf[i] = min(suf[i], suf[i + 1]);
    }
    a[n - 1] = *max_element(a.begin(), a.end());
    for(int i = n - 2; i > -1; i--){
        if(pre[i] > suf[i + 1]){
            a[i] = a[i + 1];
        }
        else{
            a[i] = pre[i];
        }
    }
    for(int i : a){
        cout << i << ' ';
    }
    return;
}
```c++
