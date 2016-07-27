# BUCT OJ 未懂题目


---

###2079

```
#include <cstdio>
#include <cstring>
#include <cmath>
#include <iostream>
#include <algorithm>
#define EPS (1e-6)
using namespace std;
double Y;
double f(double x)
{
	return 8*x*x*x*x+7*x*x*x+2*x*x+3*x+6-Y;
}
double f_(double x)
{
	return 32*x*x*x+21*x*x+4*x+3;
}
double NewtonIteration(double x,int counter=0)
{
    if(counter>10000)return -1;
    double index=f(x)/f_(x);
    return (fabs(index)<EPS)?(x-index):NewtonIteration(x-index,counter+1);
}
int main()
{
    int T;
    scanf("%d",&T);
    while(T--)
    {
        scanf("%lf",&Y);
        double ans=NewtonIteration(0);
        if(ans>=0&&ans<=100)
            printf("%.4lf\n",ans);
        else
            printf("No solution!\n");
    }
    return 0;
}
```

---

###2082

答案错误
```
#include <iostream>
#include <algorithm>
using namespace std;

typedef struct {
	int x;
	int y;
	int xy1;
	int xy2;
} data;

data enemy[1000005];

int x1,x2,y1,y2;
int max1,max2,sum;

int cmp(data a,data b)
{
	return a.xy1>b.xy1;
}

int xxyy(int a1,int b1,int a2,int b2)
{
	int x = a2 - a1;
	int y = b2 - b1;
	return x*x + y*y;
}

int main()
{
#ifdef LOCAL
	freopen("input.txt","r",stdin);
#endif
	int t;
	int n;
	cin>>t;
	while(t--)
	{
		cin>>x1>>y1>>x2>>y2;
		cin>>n;
		for(int i = 0; i < n; i++)
		{
			cin>>enemy[i].x>>enemy[i].y;
			enemy[i].xy1 = xxyy(enemy[i].x,enemy[i].y,x1,y1);
			enemy[i].xy2 = xxyy(enemy[i].x,enemy[i].y,x2,y2);
		}
		sort(enemy,enemy+n,cmp);
		sum = enemy[0].xy1;
		max2 = enemy[0].xy2;
		for(int i = 1; i < n; i++)
		{
			max1 = enemy[i].xy1;
			sum = min((max1 + max2),sum);
			max2 = max(max2,enemy[i].xy2);
		}
		cout<<sum<<endl;
	}
	return 0;
}
```

正确的

```
#include<stdio.h>
#include<string.h>
#include<math.h>
#include"stdlib.h"
#define N 100005
struct node
{
	int x,y;
	int d1,d2;       //记录平方和
}f[N];
int dis(int x1,int y1,int x2,int y2)
{
	int x=x1-x2,y=y1-y2;
	return x*x+y*y;
}
int cmp(const void*a,const void*b)
{
	return (*(struct node*)a).d1>(*(struct node*)b).d1?-1:1;
}
int min(int a,int b)
{
	return a<b?a:b;
}
int main()
{
	int T,i,n,r1,r2,ans;
	int x1,x2,y1,y2;
	scanf("%d",&T);
	while(T--)
	{
		scanf("%d%d%d%d",&x1,&y1,&x2,&y2);
		scanf("%d",&n);
		for(i=0;i<n;i++)
		{
			scanf("%d%d",&f[i].x,&f[i].y);
			f[i].d1=dis(x1,y1,f[i].x,f[i].y);
			f[i].d2=dis(x2,y2,f[i].x,f[i].y);
		}
		qsort(f,n,sizeof(f[0]),cmp);
		ans=f[0].d1;              //r1取最大值，r2=0;
		r2=f[0].d2;
		for(i=1;i<n;i++)
		{
			r1=f[i].d1;
			ans=min(ans,r1+r2);
			if(r2<f[i].d2)
				r2=f[i].d2;
		}
		ans=min(ans,r2);        //r2取最大值，r1=0即可。
		printf("%d\n",ans);
	}
	return 0;
}
```


