[题目链接](https://codeforces.com/problemset/problem/1463/B)

<br>**提示1** 想一想怎么确保总的绝对值之差的的和小于等于sum(nums)
<br>**提示2** 试着单独考虑某一项或者单独考虑某相邻两项

<br>**两种解法**
<br>
<br>解法1:我们可以想到，如果1交替出现，就一定能满足相邻项为倍数。我们可以记录偶数下标和(记为sum(o))以及奇数下标和(记为sum(j))，如果sum(o)>=sum(nums)/2,那么我们就能让偶数下标的为原数，奇数下标为1，反之亦然。容易证明，该方法一定满足总的绝对值之差的的和小于等于sum(nums)。
<br>
<br>解法2:如果每一项的差都小于等于nums[i]/2,那么总的差的绝对值和一定小于等于sum(nums)，我们可以找min(nums)为基值，后面每一项都为该数的2的n次方倍，容易证明，对于任意的基数b和任意正整数a，都存在至少一个n满足a-2^n<=a/2，且任意两项都满足倍数关系.对于n如何找呢？二分答案即可。
<br>
<br>以下是python代码(解法一)———
```python
def solve():
    n = int(input())
    nums = list(map(int, input().split()))
    s = sum(nums)
    ans = [1] * n
    cnt = 0
    for i in range(0, n, 2):
        cnt += nums[i]
    if cnt * 2 > s:
        for i in range(0, n, 2):
            ans[i] = nums[i]
    else: 
        for i in range(1, n, 2):
            ans[i] = nums[i]
    print(*ans)
```
以下是c++代码(解法一)———
```c++
void solve() {
    int n;
    cin >> n;
    vector<int>nums(n);
    vector<int>ans(n, 1);
    ll s = 0;
    for (int i = 0; i < n; i++){
        cin >> nums[i];
        s += nums[i];
    }
    ll cnt = 0;
    for (int i = 0; i < n; i += 2){
        cnt += nums[i];
    }
    if (cnt * 2 >= s){
        for (int i = 0; i < n; i += 2){
            ans[i] = nums[i];
        }
    }
    else{
        for (int i = 1; i < n; i += 2){
            ans[i] = nums[i];
        }
    }
    for (int i : ans)cout << i << ' ';
    cout << endl;
    return;
}
``` 
<br>以下是python代码(解法二)———
```python
def solve():
    n = int(input())
    nums = list(map(int, input().split()))
    ans = [0] * n
    tar = min(nums)
    for i in range(n):
        l = 0
        r = 32
        while l < r:
            mid = (l + r + 1) // 2
            if tar * pow(2, mid) > nums[i]:
                r = mid - 1
            else:
                l = mid
        ans[i] = tar * pow(2, l)
    print(*ans)
```
<br>以下是c++代码(解法二)———
```c++
void solve() {
    int n;
    cin >> n;
    vector<int>nums(n);
    vector<int>ans(n, 1);
    for (int i = 0; i < n; i++){
        cin >> nums[i];
    }
    int tar = *min_element(nums.begin(), nums.end());
    for (int i = 0; i < n; i++){
        int l = 0;
        int r = 32;
        while(l < r){
            int mid = (l + r + 1) / 2;
            ll cur = pow(2, mid);
            if (tar * cur >= nums[i]){
                r = mid - 1;
            }
            else{
                l = mid;
            }
        }
        ans[i] = pow(2, l) * tar;
    }
    for(int i : ans){
        cout << i << ' ';
    }
    cout << endl;
    return;
}
```
