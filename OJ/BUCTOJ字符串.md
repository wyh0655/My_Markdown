# BUCTOJ 字符串

标签（空格分隔）： ACM

---

[TOC]

---

###Word Amalgamation

map string 帅呆了

```
// #define DEBUG
// #define LOCAL
#include <iostream>
#include <algorithm>
#include <map>
#include <string>
using namespace std;

map <string,string> node;

int main()
{
#ifdef LOCAL
	freopen("input.txt","r",stdin);
#endif

	string s,t;
	while(cin>>s && s != "XXXXXX")
	{
		t = s;
		sort(t.begin(),t.end());
		node.insert(pair<string,string>(s,t));
	}
	while(cin>>s && s != "XXXXXX")
	{
		int flag=1; 
		map<string,string>::iterator it; 
		sort(s.begin (),s.end ()); 
		for(it = node.begin (); it != node.end(); it++) 
		{ 
#ifdef DEBUG
			cout<<s<<" "<<it->second<<endl;
#endif
			if(it->second==s) 
			{
				flag=0;
				cout<<it->first<<endl; 
			} 
		} 
		if(flag) 
			cout<<"NOT A VALID WORD"<<endl; 
		cout<<"******"<<endl; 
	}
	return 0;
}
```


---

###Fractal

这题OJ有问题，没有过的

```
#include <stdio.h>
#include <math.h>
#include <iostream>
using namespace std;

char Map[1000][1000];

void DFS(int n, int x, int y)
{
    if (n == 1)
    {
        Map[x][y] = 'X';
        return;
    }
    int size = pow(3.0, n - 2);
    DFS(n - 1, x, y);//    左上角
    DFS(n - 1, x, y + size * 2);//右上角
    DFS(n - 1, x + size, y + size);//中间
    DFS(n - 1, x + size * 2, y);//左下角
    DFS(n - 1, x + size * 2, y + size * 2);//右下角
}

int main()
{
    int n, size;
    while(scanf("%d", &n) != NULL && n != -1)
    {
        size = pow(3.0, n - 1);
        for (int i = 0; i <= size; i++)
        {
            for (int j = 0; j <= size; j++)
            {
                Map[i][j] = ' ';
            }
            Map[i][size + 1] = '\0';
        }
        DFS(n, 1, 1);
        for (int i = 1; i <= size; i++)
        {
            printf("%s\n", Map[i] + 1);
        }
        printf("-\n");
    }
    return 0;
}
```

```
#include <iostream>
using namespace std;

char Map[1000][1000];

int POW(int n)
{
	int m = 1;
	for(int i = 0; i < n; i++)
		m *= 3;
	return m;
}

void DFS(int x,int y,int n)
{
	if(n == 1)
	{
		Map[x][y] = 'X';
		return;
	}

	DFS(x,y,n/3);
	DFS(x + 2*n/3,y,n/3);
	DFS(x,y + 2*n/3,n/3);
	DFS(x + 2*n/3,y + 2*n/3,n/3);
	DFS(x + n/3,y + n/3,n/3);
	
}

int main()
{
	int n;
	while(cin>>n && n != -1)
	{
		for(int i = 0,j = 0; i < POW(n-1); i++)
		{
			for(j = 0; j < POW(n-1); j++)
				Map[i][j] = ' ';
			Map[i][j+1] = '\0';
		}
		DFS(0,0,POW(n-1));
		for(int i = 0; i < POW(n-1); i++)
			for(int j = POW(n-1); j >= 0; j--)
			{
				if(Map[i][j] != ' ')
					Map[i][j+1] = '\0';
				break;
			}


		for(int i = 0; i < POW(n-1); i++)
		{
			cout<<Map[i];
			cout<<endl;
		}
		cout<<"-"<<endl;
	}
	return 0;
}
```




