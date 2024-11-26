[题目链接](https://ac.nowcoder.com/acm/contest/95016/E)
<br>下面是python代码———:
```python
def check(i):
    i = str(i)
    ans = 0
    for j in i:
        ans += int(j)
    return ans

def solve():
    l1, r1, l2, r2 = MII()
    ma = r1 + r2
    mi = l1 + l2
    cnt = len(str(ma))
    ans = max(check(ma), check(mi))
    for i in range(0, cnt):
        s = str(ma)[:len(str(ma)) - i:]
        t = str(int(s) - 1)
        s += '9' * i
        t += '9' * i
        s = int(s)
        t = int(t)
        print(s, t)
        if ma >= s >= mi:
            ans = max(ans, check(ma))
        if ma >= t >= mi:
            ans = max(ans, check(t))
    print(ans)
```
<br>下面是c++代码———:
```c++
ll check(string s){
    ll a = 0;
    for(auto i : s){
        a += i - '0';
    }
    return a;
}

void solve(){
    ll l1, r1, l2, r2;
    cin >> l1 >> r1 >> l2 >> r2;
    ll ma = r1 + r2;
    ll mi = l1 + l2;
    string s_ma = to_string(ma);
    string s_mi = to_string(mi);
    int cnt = s_ma.size();
    ll ans = max(check(s_ma), check(s_mi));
    for(int i = 0; i < cnt; i++){
        string s = s_ma.substr(0, cnt - i);
        ll l_s = stoll(s);
        ll l_t = l_s - 1;
        string t = to_string(l_t);
        for(int j = 0; j < i; j++){
            s += '9';
            t += '9';
        }
        l_s = stoll(s);
        l_t = stoll(t);
        if(l_s >= mi && l_s <= ma){
            ans = max(ans, check(s));
        }
        if(l_t >= mi && l_t <= ma){
            ans = max(ans, check(t));
        }
    }
    cout << ans << endl;
    return;
}
```
