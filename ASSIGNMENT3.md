
class Solution:
    def findTheCity(self, n, edges, distanceThreshold):
        INF = float('inf')

        # Create distance matrix
        dist = [[INF] * n for _ in range(n)]

        for i in range(n):
            dist[i][i] = 0

        # Add edges
        for u, v, w in edges:
            dist[u][v] = w
            dist[v][u] = w

        # Floyd-Warshall algorithm
        for k in range(n):
            for i in range(n):
                for j in range(n):
                    dist[i][j] = min(
                        dist[i][j],
                        dist[i][k] + dist[k][j]
                    )

        # Find city with the fewest reachable neighbors
        result = -1
        min_count = n

        for i in range(n):
            count = 0

            for j in range(n):
                if i != j and dist[i][j] <= distanceThreshold:
                    count += 1

            if count <= min_count:
                min_count = count
                result = i

        return result
