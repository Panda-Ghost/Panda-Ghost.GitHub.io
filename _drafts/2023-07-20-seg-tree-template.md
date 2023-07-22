---
title: 各种口味的线段树板子
tags: Data Structure
---

# 各种口味的线段树板子

以下面的板子题

[Luogu P3372](https://www.luogu.com.cn/problem/P3372)

> 已知一个数列，你需要进行下面两种操作：
> 
> 1. 将某区间每一个数加上 $k$。
> 
> 2. 求出某区间每一个数的和。

为例

一律使用`namespace sg`封装

## #1 朴素易懂

```cpp
typedef long long ll;
const int maxn=100010;
namespace sg{
    struct seg{
        ll l, r, sum, flag; // 区间和 & 标记
    }s[maxn<<2];
#define L(x) s[x].l
#define R(x) s[x].r
#define S(x) s[x].sum
#define F(x) s[x].flag
#define lson (x*2)
#define rson (x*2+1)
    // 修改时下面每个函数都要修改
    void build(ll x, ll l, ll r){
        if(l==r) return s[x]=(seg){l, r, a[l], 0}, void();
        ll mid=(l+r)/2;
        build(lson, l, mid);
        build(rson, mid+1, r);
        s[x]=(seg){l, r, S(lson)+S(rson), 0};
    }
    void pushdown(ll x){
        if(F(x)){
            if(R(x)>L(x)) 
                F(lson)+=F(x), F(rson)+=F(x), 
                S(lson)+=F(x)*(R(lson)-L(lson)+1), 
                S(rson)+=F(x)*(R(rson)-L(rson)+1);
            F(x)=0;
        }
    }
    void update(ll x, ll l, ll r, ll d){
        if(l<=L(x)&&r>=R(x))
            return S(x)+=d*(R(x)-L(x)+1), F(x)+=d, void();
        pushdown(x);
        ll mid=(L(x)+R(x))/2;
        if(l<=mid) update(lson, l, r, d);
        if(r>mid) update(rson, l, r, d);
        S(x)=S(lson)+S(rson);
    }
    ll query(ll x, ll l, ll r, ll res=0){
        if(l<=L(x)&&r>=R(x))
            return S(x);
        pushdown(x);
        ll mid=(L(x)+R(x))/2;
        if(l<=mid) res+=query(lson, l, r);
        if(r>mid) res+=query(rson, l, r);
        return res;
    }
}
build(1, 1, n); // 用 a[1...n] 建树
query(1, l, r); // 查询 a[l...r] 的和
update(1, l, r, k); // 将 a[l...r] 的元素加 k
```

## #2 扩展性强

```cpp
typedef long long ll;
const int maxn=100010;
namespace sg{
    struct Q{ // 标记区
        ll tag;
        Q(ll tag=0): tag(tag){}
        void operator+=(const Q &q){ tag+=q.tag; } // tag 的叠加
    };
    struct P{ // 维护的数据区
        ll sum;
        P(ll sum=0): sum(sum){}
        void push(const Q &q, int l, int r){ sum+=q.tag*(r-l+1); } // 用 tag 修改
        void init(int x){ sum=a[x]; } // 单点初始化
    };
    P operator&(const P &a, const P &b){ // 区间并
        return P(a.sum+b.sum);
    }
    // 修改时只修改上方
    P p[maxn<<2];
    Q q[maxn<<2];
#define lson o*2, l, (l+r)/2
#define rson o*2+1, (l+r)/2+1, r
    void up(int o, int l, int r){
        if(l<r) p[o]=p[o*2]&p[o*2+1];
    }
    void push(const Q &v, int o, int l, int r){
        q[o]+=v;
        p[o].push(v, l, r);
    }
    void down(int o, int l, int r){
        push(q[o], lson); push(q[o], rson);
        q[o]=Q();
    }
    void build(int o=1, int l=1, int r=n){
        if(l==r) p[o].init(l);
        else{ build(lson); build(rson); }
        up(o, l, r);
    }
    P query(int ql, int qr, int o=1, int l=1, int r=n){
        if(ql>r||l>qr) return P();
        if(ql<=l&&r<=qr) return p[o];
        down(o, l, r);
        return query(ql, qr, lson)&query(ql, qr, rson);
    }
    void update(int ql, int qr, const Q& v, int o=1, int l=1, int r=n){
        if(ql>r||l>qr) return;
        if(ql<=l&&r<=qr){ push(v, o, l, r); return; }
        down(o, l, r);
        update(ql, qr, v, lson); update(ql, qr, v, rson);
        up(o, l, r);
    }
}
build(); // 用 a[1...n] 建树
query(l, r).sum; // 查询 a[l...r] 的和
update(l, r, Q(k)); // 将 a[l...r] 的元素加 k
```
