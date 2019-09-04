> > 堆排序

```c++
#include <iostream>
#include <algorithm>
using namespace std;

void sink(int a[],int index,int n)
{
	int leftchild = 2*index + 1;//左节点下标
	int rightchild = 2*index +2;//右结点下标
	int present = index;//要调整的节点下标

	//下沉左边
	if(leftchild < n && a[leftchild] > a[present])
	{
		present = leftchild;
	}
	//下沉右边
	if(rightchild < n && a[rightchild] > a[present])
	{
		present = rightchild;
	}
	//如果下标不相等，证明被调换过了
	if(present != index)
	{
		int temp = a[index];
		a[index] = a[present];
		a[present] = temp;

		//继续下沉
		sink(a, present,n);
	}
}

void buildheap(int a[],int n)
{
	//堆是完全二叉树
	for(int i = n/2; i >= 0; i--)
	{
		sink(a,i,n);
	}
}

void sort(int a[],int n)
{
	//构建堆
	buildheap(a,n);
	for(int i = n - 1; i>0; i--)
	{
		//将堆顶元素与末位元素调换
		int temp = a[0];
		a[0] = a[i];
		a[i] = temp;
		n--;//数组长度-1 隐藏堆尾元素
		sink(a,0,n);//将堆顶元素下沉 目的是将最大的元素浮到堆顶来
	}
}

int main()
{
	int data[8] = {4,6,3,2,1,5,8,0};
	int size = sizeof(data)/sizeof(int);
	sort(data,size);
	for(int i = 0; i < size; i++)
	{
		std::cout << data[i] << " ";
	}
	cout << endl;
	return 0;
}
```

> > 已排序的数组，但是会不知道在什么位置旋转（1,2,4,6,7——>4,6,7,1,2），找某个数字

```c++
#include <iostream>

using namespace std;

int search(int a[],int n,int target)
{
	int first = 0;
	int last  = n;
	while(first != last)
	{
		const int mid = first + (last - first) / 2;
		if(a[mid] == target)
			return mid;
		if(a[first] <= a[mid])
		{
			if(a[first] <= target && target < a[mid])
				last = mid;
			else
				first = mid + 1;
		}
		else
		{
			if(a[mid] < target && target <= a[last - 1])
				first = mid + 1;
			else
				last = mid;
		}
	}
	return -1;
}

int main()
{
	int data[6] = {4,6,7,1,2};
	int size = sizeof(data)/sizeof(int);
	cout << search(data,size,1) << endl;
	return 0;
}
```

> > 在已排序的两个数组中找中位数

```c++
#include <iostream>
#include <algorithm>

using namespace std;

int find_kth(int a[],int m,int b[],int n,int k)
{
	if(m > n)
		return find_kth(b,n,a,m,k);
	if(m == 0)
		return b[k - 1];
	if(k == 1)
		return min(a[0],b[0]);

	int ia = min(k/2,m);
	int ib = k - ia;
	if(a[ia - 1] < b[ib - 1])
		return find_kth(a+ia,m-ia,b,n,k-ia);
	else if(a[ia - 1] > b[ib - 1])
		return find_kth(a,m,b+ib,n-ib,k-ib);
	else
		return a[ia - 1];
}

double findMidSorted(int a[],int m,int b[],int n)
{
	int total = m+n;
	if(total & 0x1)
	{
		return find_kth(a,m,b,n,total/2 + 1);
	}
	else
	{
		return (find_kth(a,m,b,n,total/2) + find_kth(a,m,b,n,total/2 + 1)) / 2.0;
	}
	return 0;
}

int main()
{
	int d1[5] = {1,3,5,7,9};
	int d2[3] = {2,4,6};
	cout << findMidSorted(d1,5,d2,3) << endl;
	return 0;
}
```

> > 从两个已经排序好的数组中，找第K大的数字

```c++
#include <iostream>

using namespace std;

int search(int a[],int m,int b[],int n,int k)
{
	int j = 0;
	int i = 0;
	int cur = 0;
	while(i < n && j < m)
	{
		if(a[i] < b[j])
		{
			cur++;
			if(cur == k)
				return a[i];
			i++;
		}
		else
		{
			cur++;
			if(cur == k)
				return b[j];
			j++;
		}
	}
	while(i<m)
	{
		cur++;
		if(cur == k)
			return a[i];
		i++;
	}
	while(j < n)
	{
		cur++;
		if(cur == k)
			return b[j];
		j++;
	}
	return -1;

}

int main()
{

	int d1[5] = {1,3,5,7,9};
	int d2[3] = {2,4,6};
    //第五个参数表示第k个
	cout << search(d1,5,d2,3,6) << endl;
	return 0;
}
```

> > 合并两个分别排序好的数组

```
#include<iostream>
using namespace std;
 
int *SortArry(int *StrA,int lenA, int *StrB, int lenB)
{
  if (StrA == NULL || StrB == NULL)
  return NULL;
 
 int *StrC = new int[lenA + lenB+1];
 
 int i = 0, j = 0, k = 0;
 while (i < lenA && j < lenB)
 {
     if (StrA[i] < StrB[j])
         StrC[k++] = StrA[i++];
     else
	  {
	   StrC[k++] = StrB[j++];
	  }
 }
 
 while (i<lenA)
	 {
	  StrC[k++] = StrA[i++];
	 }
 
 while (j<lenB)
	 {
	  StrC[k++] = StrB[j++];
	 }
 
return StrC;
}

int main()
{
 int array1[] = { 1, 3, 5, 7, 9 };
 int array2[] = { 2, 4, 6, 8, 10 };
 int lenA = sizeof(array1) / sizeof(int);
 int lenB = sizeof(array2) / sizeof(int);
 int *ret = SortArry(array1, lenA, array2, lenB);
 for (int i = 0; i < (lenA + lenB); i++)
 	cout << ret[i] <<' ';
 cout << endl;
 return 0;
}
```

