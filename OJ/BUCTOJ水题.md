# BUCTOJ水题


### 五子棋

```
#define DEBUG
#define LOCAL
#include <iostream>
using namespace std;

int main()
{
#ifdef LOCAL
	freopen("input.txt","r",stdin);
#endif
	int a[10][10] = {0};
	int x,y;
	int startx = -1,starty = -1;
	for(int i = 0; i < 4; i++)
	{
		cin>>x>>y;
		a[x][y] = 1;
	}
#ifdef DEBUG
	for(int i = 0; i < 10; i++)
	{
		for(int j = 0; j < 10; j++)
			cout<<a[i][j]<<" ";
		cout<<endl;
	}
#endif
	for(int i = 0; i < 10; i++)
	{
		for(int j = 0; j < 10; j++)
			if(a[i][j])
			{
				startx = i;
				starty = j;
				break;
			}
		if(startx != -1)
			break;
	}
#ifdef DEBUG
	cout<<startx<<" "<<starty<<endl;
#endif
	if(a[startx][starty+1] || a[startx][starty+2])
	{
		if(starty > 5)
		{
			cout<<startx<<" 5"<<endl;
			return 0;
		}
		else
			for(int i = 0; i < 5; i++)
			{
				if(!a[startx][starty])
				{
					cout<<startx<<" "<<starty<<endl;
					return 0;
				}
				starty++;
			}
	}
	if(a[startx+1][starty+1] || a[startx+2][starty+2])
	{
		if(starty > 5)
		{
			cout<<startx-1<<" 5"<<endl;
			return 0;
		}
		else
			for(int i = 0; i < 5; i++)
			{
				if(!a[startx][starty])
				{
					cout<<startx<<" "<<starty<<endl;
					return 0;
				}
				startx++;
				starty++;
			}
	}

	if(a[startx+1][starty] || a[startx+2][starty])
	{
		if(startx > 5)
		{
			cout<<"5 "<<starty<<endl;
			return 0;
		}
		else
			for(int i = 0; i < 5; i++)
			{
				if(!a[startx][starty])
				{
					cout<<i<<" "<<starty<<endl;
					return 0;
				}
				startx++;
			}
	}

	if(a[startx+1][starty-1] || a[startx+2][starty-2])
	{
		if(startx > 5)
		{
			cout<<"5 "<<starty<<endl;
			return 0;
		}
		else
			for(int i = 0; i < 5; i++)
			{
				if(!a[startx][starty])
				{
					cout<<i<<" "<<starty<<endl;
					return 0;
				}
				startx++;
				starty--;
			}
	}
	return 0;
}
```

---

### 倒着数数

```
#include <iostream>
#include <cstdio>
using namespace std;

int main()
{
	int a[] = {	0,10,90,80,60,
				1,11,91,81,61,
				9,19,99,89,69,
				8,18,98,88,68,
				6,16,96,86,66};
	int n;
	int i;
	int m[25];
	cin>>n;
	for(i = 0; i < n; i++)
		cin>>m[i];
	for(i = 0; i < 25; i++)
	{
		if(m[0] == a[i])
			break;
	}
	if(m[1] == a[i+1])
		m[n] = a[i+n];
	else if(m[1] == a[i-1])
		m[n] = a[i-n];
	printf("%02d\n",m[n]);
	return 0;
}

```



