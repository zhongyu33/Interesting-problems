[题目链接](https://atcoder.jp/contests/abc380/tasks/abc380_d)
<br>下面是python代码————:
```python
def change(i):
    if i >= "a":
        return i.upper()
    return i.lower()
    
def dfs(i):
    if i <= n:
        return s[i - 1]
    c = math.floor(math.log2(i / n))
    while n * pow(2, c) > i:
        c -= 1
    if n * pow(2, c) == i:
        if c % 2 == 0:
            return s[-1]
        return change(s[-1])
    return change(dfs(i - n * pow(2, c)))
    
def solve():
    s = input().strip()
    n = len(s)
    m = int(input())
    a = list(map(int, input().split()))
    ans = []
    for i in a:
        ans.append(dfs(i))
    print(*ans)
```
<br>下面是c++代码:
```c++
char change(char i) {
    if (i >= 'a') {
        return toupper(i);
    }
    return tolower(i);
}

char dfs(ll i, ll n, const string& s) {
    if (i <= n) {
        return s[i - 1];
    }
    ll p;
    ll c = log2(i * 1.0 / n);
    p = pow(2, c) * n;
    while (p > i) {
        c--;
        p = pow(2, c) * n;

    }
    p = n * pow(2, c);
    
    if (p == i) {
        if (c % 2 == 0) {
            return s[n - 1];
        }
        return change(s[n - 1]);
    }
    return change(dfs(i - p, n, s));
}
void solve(){
    string s;
    cin >> s;
    ll n = s.size();
    ll m;
    cin >> m;
    vector<ll> a(m);
    for (ll i = 0; i < m; i++) {
        cin >> a[i];
    }

    vector<char> ans;
    for (ll i : a) {
        ans.push_back(dfs(i, n, s));
    }

    for (char c : ans) {
        cout << c << " ";
    }
    cout << endl;
    return;
}
```
