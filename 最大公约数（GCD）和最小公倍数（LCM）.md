欧几里得算法实现GCD和LCM
	从数学的角度来看，欧几里得算法基于这样一个事实：两个整数a和b（假设a > b）的最大公约数等于a除以b的余数c和b之间的最大公约数。也就是说，GCD(a, b) = GCD(b, c)，其中c = a % b。**该算法的核心思想是将大问题分解为小问题，通过不断缩小问题规模来解决问题。重复执行余数操作直到余数为零，最后非零余数的除数就是这两个数的最大公约数。
$$
	求得GCD之后，LCM满足LCM(a,b)=∣a×b∣/GCD(a,b)
$$
```
#include<stdio.h>
int main()
{
	int m;
	int n;
	int temp;
	int q;
	printf("从大到小任意输入两个数:");
	scanf("%d %d",&m,&n);
	q = m*n;
	//最大公约数
		while(n!=0)
		{
			temp = m%n;
			m = n;
			n = temp;//每次递归调用中，m取当前的n值，n取m%n的余数。
		}
		printf("最大公约数是%d",m);
	//最小公倍数
	printf("最小公倍数是%d",q/m);
	return 0;
}
```
