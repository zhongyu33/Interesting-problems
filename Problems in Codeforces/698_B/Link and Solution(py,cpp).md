[题目链接](https://codeforces.com/problemset/problem/698/B)

**提示 1：** 这个图有什么特点？

**提示 2：** 如果只有一个连通块，应该怎么处理？

**提示 3：** 如果有多个连通块呢？

这个图有一个特点，就是每一个点都恰好连出来一条边。如果这些边是没有方向的，则考虑每一个连通块，点数等于边数，因此恰好有一个环。

如果只有一个连通块，那么我们只需使得这个环大小为 $1$ 即可，因此在大小非 $1$ 的时候进行操作即可。

而如果有多个连通块呢？

首先，如果某个连通块对应的环大于 $1$ ，则这个环不得不进行一次操作，因为目标是整个图中只有一个大小为 $1$ 的环。

接下来可以通过一次操作让一个环指向另一个环，最后构造成树。而这一步跟前面的缩小环是可以同时进行的。

于是，我们只需确认最后环的位置再进行操作即可。

整体的逻辑是这样：我们有一系列大小不一的环，每次操作可以将一个环不再是环，并连到另一个上，或者使得一个环大小变为 $1$ 。

于是操作次数至少为环的个数 $-1$ ，因为至少这么多次才能使得环所在的连通块两两相连。而如果没有环大小为 $1$ ，则应当再进行一个“缩环”操作。

因此，如果有一个点本身形成了自环，则我们选其作为根节点，因为这样可以避免最后一次环大小变为 $1$ 的操作。否则，我们任选一个在环内的点作为根节点即可。

整体只需 DFS 等图遍历的方法。

时间复杂度为 $\mathcal{O}(n)$ 。

### 具体代码如下——

Python 做法如下——

```Python []
def main():
    n = II()
    nums = LGMI()

    rt = -1
    for i in range(n):
        if nums[i] == i:
            rt = i

    ans = 0
    vis = [-1] * n
    for i in range(n):
        if vis[i] == -1:
            u = i
            while vis[u] == -1:
                vis[u] = i
                u = nums[u]
            
            if vis[u] == i and u != rt:
                ans += 1
                if rt >= 0:
                    nums[u] = rt
                else:
                    nums[u] = u
                    rt = u

    print(ans)
    print(' '.join(str(x + 1) for x in nums))
```

C++ 做法如下——

```cpp []
int find(int i, vector<int> &g){
    if(g[i] == i){
        return i;
    }
    return g[i] = find(g[i], g);
}

void solve(){
    int n;
    cin >> n;
    int ans = 0;
    vector<int>a(n);
    bool f = false;
    int root = -1;
    for(int i = 0; i < n; i++){
        cin >> a[i];
        if(a[i] == i + 1){
            if(f){
                a[i] = root;
                ans += 1;
            }
            else{
                f = true;
                root = i + 1;
            }
        }
    }
    vector<int>g(n + 1);
    for(int i = 0; i < n + 1; i++){
        g[i] = i;
    }
    for(int i = 0; i < n; i++){

        if(i + 1 == root) continue;
        int x = find(i + 1, g);
        int y = find(a[i], g);
        if(x == y){
            if(!f){
                a[i] = i + 1;
                root = i + 1;
                ans++;
                f = true;
            }
            else{
                ans += 1;
                a[i] = root;
            }
        }
        x = find(i + 1, g);
        y = find(a[i], g);
        if(x < y){
            g[y] = x;
        }
        if (x > y){
            g[x] = y; 
        }
    }
    cout << ans << endl;
    for(int i : a){
        cout << i << ' ';
    }
    cout << endl;
    return;
}  
```
