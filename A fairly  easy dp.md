/*
    Based on "E. By Elevator or Stairs?" of Codeforces Round #595 (Div. 3);
    This dp is basicly: store the less value of the given possibilitys.
    The thing about this problem is it's transitions. Instead of going just (i+1), u have to go (i+1, 1) and (i+1, 0),
        because it can go (stair stair), (stair elevator), (elevator stair), (elevator elevator).
    So this is just a reminder, go's through all possiblites.
*/

#include <bits/stdc++.h>
using namespace std;
 
int n, k;
vector<int> a, b;
 
int mat[200000][2];
// 1 - elevador || 0 - stairs
 
 
int dp(int i, int x)
{	if(i == 0){ if(x == 1) return mat[i][x] = k; else return mat[i][x] = 0; }
	if(mat[i][x] != -1) return mat[i][x];
	
	int p, q;
	if(x == 0)
	{	p = dp(i-1, 1) + a[i];
		q = dp(i-1, 0) + a[i];
	}
	
	if(x == 1)
	{	p = dp(i-1, 1) + b[i];
		q = dp(i-1, 0) + b[i] + k;
	}
	
	return mat[i][x] = min(p, q);
}
	
 
int main()
{	cin >> n >> k;
	a.resize(n); b.resize(n);
	
	for(int i = 0; i < n; i++) for(int j = 0; j < 2; j++) mat[i][j] = -1;
	
	a[0] = 0; for(int i = 1; i < n; i++) cin >> a[i];
	b[0] = 0; for(int i = 1; i < n; i++) cin >> b[i];
	
	dp(n-1, 0); dp(n-1, 1); 
	for(int i = 0; i < n; i++)
	cout << min(mat[i][0], mat[i][1]) << ' ';
	cout << endl;
}

        
