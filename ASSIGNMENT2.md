from collections import defaultdict
from fractions import Fraction

t = int(input())

for _ in range(t):

    n = int(input())

    graph = defaultdict(list)

    for i in range(n - 1):
        u, v = map(int, input().split())
        graph[u].append(v)
        graph[v].append(u)

    g, k = map(int, input().split())

    guesses = set()

    for i in range(g):
        u, v = map(int, input().split())
        guesses.add((u, v))

    # Root the tree at node 1
    parent = {1: 0}
    stack = [1]
    score = 0

    while stack:
        u = stack.pop()

        for v in graph[u]:

            if v == parent[u]:
                continue

            parent[v] = u
            stack.append(v)

            if (u, v) in guesses:
                score += 1

    # Calculate score for every possible root
    scores = {1: score}
    stack = [1]

    while stack:
        u = stack.pop()

        for v in graph[u]:

            if parent.get(v) == u:

                new_score = scores[u]

                if (u, v) in guesses:
                    new_score -= 1

                if (v, u) in guesses:
                    new_score += 1

                scores[v] = new_score
                stack.append(v)

    # Count winning roots
    winning = 0

    for node in scores:
        if scores[node] >= k:
            winning += 1

    # Reduce fraction
    answer = Fraction(winning, n)

    print(str(answer.numerator) + "/" + str(answer.denominator))
