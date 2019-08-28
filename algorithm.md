> > 在一个长度为 n 的数组里的所有数字都在 0 到 n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字是重复的，也不知道每个数字重复几次。请找出数组中任意一个重复的数字.

```c++
#include <iostream>
#include <algorithm>
using namespace std;

void change(int nums[], int i, int j) {
    int t = nums[i];
    nums[i] = nums[j];
    nums[j] = t;
}

int main(int argc, char const *argv[])
{
	
	int nums[6] = {2, 3, 1, 0, 2, 5};
	int size = sizeof(nums)/sizeof(int);
	int copy;
	for (int i = 0; i < size; i++) {
        while (nums[i] != i) {
            if (nums[i] == nums[nums[i]]) {
                copy = nums[i];
                break;
            }
            change(nums, i, nums[i]);
        }
    }
    cout << copy << endl;
	return 0;
}
```

> > 找出无序数组的中位数

```c++
#include <iostream>

using namespace std;

int PartSort(int *arr, int start, int end)
{
    int left = start;
    int right = end;
    int key = arr[end];   //选取关键字
    while (left < right)
    {
        while (left < right && arr[left] <= key)  //左边找比key大的值
        {
            ++left;
        }
        while (left < right && arr[right] >= key)  //右边找比key小的值
        {
            --right;
        }
        if (left < right)
        {
            swap(arr[left], arr[right]);  //找到之后交换左右的值
        }
    }
    swap(arr[right], arr[end]);
    return left;
}

int GetMidNumNoSort1(int *arr,int size)
{
    //assert(arr);
    int start = 0;
    int end = size - 1;
    int mid = (size - 1) / 2;
    int div = PartSort(arr,start,end);
    while (div != mid)
    {
        if (mid < div)   //左半区间找
            div = PartSort(arr, start, div - 1);
        else    //左半区间找
            div = PartSort(arr, div + 1, end);
    }
    return arr[mid];   //找到了
}

int main()
{
	int arr[6] = {0,1,2,4,3,4};
	cout << GetMidNumNoSort1(arr,6) << endl;

	return 0;
}
```

> > 去掉字符串中的空格

```c++
#include <iostream>

using namespace std;

int main()
{
 	char str[40] = " abc 123 456 ";
 	int num = 0;
	 int i;
 	for(i = 0; str[i] != '\0'; ++i)
 	{
 		if(str[i] == ' ')
	 		++num;
		else
 			str[i-num] = str[i];
 	}
 	str[i-num] = '\0';
 	printf("%s\n",str);
 }
```

> > 给定一个二维数组，其每一行从左到右递增排序，从上到下也是递增排序。给定一个数，判断这个数是否在该二维数组中。

```
Consider the following matrix:
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

Given target = 5, return true
Given target = 20, return false
```

```c++
#include <iostream>
#include <vector>

using namespace std;

bool isExist(std::vector<std::vector<int>> martix, int m, int n, int target)
{
	int r = 0, c = n - 1; // 从右上角开始
	while(r <= m - 1 && c >= 0)
	{
		if(target == martix[r][c])
		{
			return true;
		}
		else if(target > martix[r][c])
		{
			r++;
		}
		else
		{
			c--;
		}
	}
	return false;
}

int main()
{
	int m = 5;
	int n = 5;
	std::vector<std::vector<int>> arr = {{1,4,7,11,15},{2,5,8,12,19},{3,6,9,16,22},{10,13,14,17,24},{18,21,23,26,30}};
	cout << isExist(arr,m,n,20) << endl;
	return 0;
}
```

