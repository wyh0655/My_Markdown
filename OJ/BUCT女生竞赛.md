# BUCT女生竞赛

###A

```
#include <iostream>
#include <cmath>
using namespace std;
int IsKind(int n)
{
	int i, sum = 0;
	for(i=1; i<=(int)sqrt(n); i++)
		if(n%i == 0)
			sum += i + n/i;
	return sum;
}
int main()
{
	int n, m, t;
	cin>>t;
	while(t--)
	{
		cin>>n>>m;
		if(IsKind(m) == IsKind(n))
			cout<<"YES"<<endl;           
		else
			cout<<"NO"<<endl;
	}   
	return 0;
}
```

---

###B

```
#include <iostream>
using namespace std;

int main()
{
	int n;
	while(cin>>n)
	{
		int sum = 1;
		for(int i = 1; i < n; i++)
		{
			sum = (sum+1)*2;
		}
		cout<<sum<<endl;
	}
	return 0;
}
```

---

###C

超时
1338题

```
#include <iostream>
#include <cstring>
#include <string>
#include <algorithm>
#include <map>
using namespace std;

int main()
{
	char str[101],odr[101];
	int len;
	cin>>str;
	len = strlen(str);
	strcpy(odr,str);
	sort(odr,odr+len);
	map<string ,int> mp;						// 一一对应关系
	int k = 1;
	while(1)
	{
		if(mp[string(odr)] == 0)
			mp[string(odr)]=k++;
		if(!next_permutation(odr,odr+len))		// 生成全排列
			break;
	}
	cout<<mp[string(str)]<<endl;
	return 0;
}
```

---

###D

2784题

```

```

---

###E

```
// #define LOCAL
#include <iostream>
#include <cstring>
#include <cstdio>
using namespace std;

int main()
{
#ifdef LOCAL
	freopen("input.txt","r",stdin);
#endif
	int m,n,count,flag[101];
	char course[101][101];
	cin>>m;
	while(m--)
	{
		memset(flag,0,sizeof(flag));
		count = 0;
		cin>>n;
		for(int i = 0; i < n; i++)
		{
			for(int j = 0; j < n; j++)
			{
				cin>>course[i][j];
				if(course[i][j] == '1')
					flag[j] = 1;
			}
		}
		for(int i = 0; i < n; i++)
			if(flag[i] != 1)
			{
				if(count)
					cout<<" ";
				count++;
				cout<<i;
			}
		cout<<endl;
	}
	return 0;
}
```

---

###F

```
// #define LOCAL
#include <iostream>
#include <cstring>
using namespace std;

int x[16] = {0,1,0,1,1,0,1,0,0,1,0,1,1,0,1,0};

int main()
{
#ifdef LOCAL
	freopen("input.txt","r",stdin);
#endif
	int n;
	int less[16],num[16];
	int sum;
	cin>>n;
	while(n--)
	{
		memset(less,0,sizeof(less));
		for(int i = 0; i < 16; i++)
		{
			cin>>num[i];
			if(num[i] == 16)
				sum = x[i];

		}
		for(int i = 0; i < 16; i++)
		{
			for(int j = 0; j < i; j++)
				if(num[j] < num[i])
					less[i]++;
		}
		for(int i = 0; i < 16; i++)
			sum += less[i];
		if(sum%2)
			cout<<"False"<<endl;
		else
			cout<<"True"<<endl;
	}
	return 0;
}
```

---


