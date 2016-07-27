# C++函数练习


###字符串反向

```
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

int main()
{
	string str;
	int t;
	cin>>t;
	while(t--)
	{
		cin>>str;
		reverse(str.begin(),str.end());
		cout<<str<<endl;
	}
	return 0;
}
```

###深搜

```
#include <iostream>
using namespace std;
int m;
void dfs(int b)
{
	if(b>=3)
	{
		dfs(b-3);
	}
	if(b>=2)
	{
		dfs(b-2);
	}
	if(b>=1)
	{
		dfs(b-1);
	}
	if(b==0)
	m++;
}
int main()
{
	int n,a;
	cin>>n;
	while(n--)
	{
		m=0;
		cin>>a;
		dfs(a);
		cout<<m<<endl;
	}
	return 0;
}
```

---




