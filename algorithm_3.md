> > 螺旋矩阵

```C++
#include <iostream>
#include <iomanip>
#include <vector>

using namespace std;

int main()
{
	int n = 6;
	int m = 6;
	vector<vector<int>> num(6,vector<int>(6,0));
	int count = 1;
	int x = 0, y = 0;
	int dx = 0, dy = 1;
	while (count <= m*n)
	{
		num[x][y] = count;
		x += dx;
		y += dy;
		if (dy == 1 && (y >= n - 1 || num[x][y + 1] != 0))
		{
			dx = 1;
			dy = 0;
		}
		else if (dx == 1 && (x >= m - 1 || num[x + 1][y] != 0))
		{
			dx = 0;
			dy = -1;
		}
		else if (dy == -1 && (y <= 0 || num[x][y - 1] != 0))
		{
			dx = -1;
			dy = 0;
		}
		else if (dx == -1 && (x <= 0 || num[x - 1][y] != 0))
		{
			dx = 0;
			dy = 1;
		}
		count++;
	}

	for (int i = 0; i < m; i++)
	{
		for (int j = 0; j < n; j++)
		{
			cout << setw(4) << num[i][j];
		}
		cout << endl;
	}
	
	system("PAUSE");
	return 0;
}
```

### 结果：

```
1   2  3  4  5  6
20 21 22 23 24  7
19 32 33 34 25  8
18 31 36 35 26  9
17 30 29 28 27 10
16 15 14 13 12 11

```

