/* 
    Problem D. Subarray Sorting of Educational Codeforces Round 67 (Rated for Div. 2);
    Here we have a Segment tree used as a auxliary data structure.
    What is wanted is to check  if it's possible to transform the sequence of integers 'a' in another sequence 'b'.
        The only modification permited is to use sort on whaterver querry on the sequence a, is possible to do this unlimited times.
    So basicly, afther thinking on the problem, what he wants it's to check if the elements b[i] on 'a' is the lower element 
        between 0 and pos of b[i] on 'a'; And we can use a "Seg" to do this.
    Look, a Seg has tree elmentary things that need to be on check:
        elements - What the elements means? Here it means the elements of 'b';
        value - what the value of each element means? Here it means the position of 'b' on 'a';
        moments - what each moment on a "Seg" mmeans? Here it means the position of the actual first elements of 'b' on 'a';
            Obs: it's used a queue to store the positions of the 'b's on 'a', to make the update easier latter on;
*/

#include <bits/stdc++.h>
using namespace std;
 
class Segtree
{	public: vector<int> st; int n;
	Segtree(int n)
	{	this->n = n; st.resize(4*n+50, 1e8); }
	
	void Update(int v, int tl, int tr, int pos, int value)
	{	if(tl == tr)
		{	st[v] = value; return; }
		
		int mid = tl+tr; mid>>=1;
		int son = v<<1;
		if(pos < mid) Update(son, tl, mid, pos, value);
		else Update(son+1, mid+1, tr, pos, value);
		
		st[v] = min(st[son], st[son+1]);
	}
	
	int Querry(int v, int tl, int tr, int l, int r)
	{	if(l > r) return 1e8;
		if(tl == l && tr == r) return st[v];
		
		int mid = tl+tr; mid>>=1;
		int son = v<<1;
		int a = Querry(son, tl, mid, l, min(r, mid));
		int b = Querry(son+1, mid+1, tr, max(mid+1, l), r);
		
		return min(a, b);
	}
};
 
 
int main()
{	int t; cin >> t;
	while(t--, t > -1)
	{	int n; cin >> n;
		
		unordered_map<int, queue<int> > p;
		vector<int> a, b; 
		p.clear(); a.clear(); b.clear();
		a.resize(n); b.resize(n);
		for(int i = 0; i < n; i++)
		{	cin >> a[i];
			p[--a[i]].push(i);
		} 
		
		for(int i = 0; i < n; i++)
		{	cin >> b[i]; b[i]--; }
		
		Segtree* h = new Segtree(n);
		for(int i = 0; i < n; i++)
			if(p.find(i) != p.end() && !p[i].empty())
			{	h->Update(1, 0, n, i, p[i].front()); }
		
		bool truth = true;
		for(int i = 0; i < n; i++)
		{	if(p[b[i]].empty())
			{	truth = false; break; }
			
			int pos = p[b[i]].front(); int k;
			if(h->Querry(1, 0, n, 0, b[i]) < pos)
			{	truth = false; break; }
		
			p[b[i]].pop();
			h->Update(1, 0, n, b[i], p[b[i]].empty() ? 1e8 : p[b[i]].front());
		}
		
		cout << (truth == true ? "YES" : "NO") << endl;
	} return 0;
}
