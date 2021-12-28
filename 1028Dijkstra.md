## Description
给定n(n<=500)个顶点,以及E(E<=10000)条边，使用迪杰斯特拉算法计算顶点s到顶点t的最短路径.

## Input
第一行输入T表示有T组数据。每组数据第一行输入n、E、s、t，分别表示顶点数、边数、顶点s以及顶点t. 接下来
输入E行每行三个正整数u(1<=u<=n)、v(1<=v<=n)、w，表示顶点u到顶点v之间无向边长度w（可能有重边）。

## Output
输出T行正整数，第i行表示第i组数据s到达t的最短路径长度。若s无法到达t国，输出-1.

## Sample Input
3

2 2 1 2

1 2 1

1 2 2

3 1 1 3

2 3 1

3 3 1 3

1 2 1

1 2 3

2 3 1

## Sample Output
1

-1

2


## Solution

```C++
int Dijkstra(int edge[][505], int nv, int s, int t)
{
	bool* visit = new bool[nv + 1];
	int* dist = new int[nv + 1];
	for (int i = 1; i <= nv; i++)
	{
		visit[i] = false;
		dist[i] = edge[s][i];
	}
	visit[s] = true;
	dist[s] = 0;
	for (int i = 1; i < nv; i++)
	{
		int u; // 找到当前dist最小的顶点,
		int min_dist = INF;
		for (int j = 1; j <= nv; j++)
			if (!visit[j] && dist[j] < min_dist)
			{
				min_dist = dist[j];
				u = j;
			}
		visit[u] = true;
		for (int k = 1; k <= nv; k++) //对其他所有未访问的点relax
			if (!visit[k])
				dist[k] = min(dist[k], dist[u] + edge[u][k]);
	}
	if (dist[t] == INF)
		return -1;
	else
		return dist[t];
}


int M;
int NV, NE, S, T;
int E[505][505];
int main()
{
	cin >> M;
	for (int m = 0; m < M; m++)
	{
		cin >> NV >> NE >> S >> T;
		for (int i = 0; i < 505; i++)
			for (int j = 0; j < 505; j++)
				E[i][j] = INF;
		for (int i = 0; i < NE; i++)
		{
			int u, v, w;
			cin >> u >> v >> w;
			E[u][v] = min(E[u][v], w);
			E[v][u] = min(E[v][u], w);
		}

		//for (int i = 1; i <= NV; i++)
		//{
			//for (int j = 1; j <= NV; j++)
				//cout << E[i][j]<<' ';
			//cout << endl;
		//}
		

		cout << Dijkstra(E, NV, S, T) << endl;
	}
}
```
