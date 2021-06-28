# max-pairs
#include <bits/stdc++.h>
using namespace std;
#define ull unsigned long long
#define ll long long
#define ld long double
#define MOD 1000000007
#define vec vector<int>
#define vecll vector<ll>
#define pb push_back
#define f(i,l,n) for(int i=l;i<n;i++)
#define fll(i,l,n) for(ll i=l;i<n;i++)
#define regstuff                \
    int n;                      \
    cin >> n;                   \
    vec A(n);                   \
    for (int i = 0; i < n; i++) \
        cin >> A[i];
#define fast                          \
    ios_base::sync_with_stdio(false); \
    cin.tie(NULL);
vec noprimes(1000001);

void seive(vec &primes, int n)
{
   //gives a prifix array of number of primes as well
    vector<bool> ntprimes(n + 1, false);
    ntprimes[0] = ntprimes[1] = true;
    for (int i = 2; i * i <= n; i++)
    {
        if (!ntprimes[i])
        {
            for (int j = i * i; j <= n; j += i)
            {
                ntprimes[j] = true;
            }
        }
    }
    int x = 0;
    for (int i = 2; i <= n; i++)
    {
        if (!ntprimes[i])
        {
            primes.pb(i);
            x++;
            noprimes[i] = x;
        }
        else
            noprimes[i] = x;
    }
}

ll fpow(ll x, ll n)
{
    ll res = 1;
    while (n)
    {
        if (n % 2 == 0)
        {
            n = n / 2;
            x = x * x;
        }
        else
        {
            res *= x;
            n--;
        }
    }
    return res;
}

int main()
{
    fast 
    ll n;
    cin>>n;
    ll k;
    cin>>k;
    vecll pairsz(k);
    fll(i,0,k)cin>>pairsz[i];
    ll val=fpow(2,n);
    vector<vecll> A(pairsz[k-1]+1);
    fll(i,1,val+1)
    {
        ll x=1;
        vecll ans;
        fll(j,0,n)
        {
            if(x&i)
            {
                ans.pb(j+1);
            }
            x=x<<1;
        }
        fll(j,0,pairsz.size())
        {
            if(pairsz[j]==ans.size())
            {
                fll(k,0,ans.size())
                {
                    A[pairsz[j]].pb(ans[k]);
                }
                break;
            }
        }
        
    }
    fll(i,1,A.size())
    {
        fll(j,0,A[i].size())
        {
            cout<<A[i][j]<<" ";
            if(((j+1)%i)==0)
            cout<<endl;
        }
    }
    return 0;
}
