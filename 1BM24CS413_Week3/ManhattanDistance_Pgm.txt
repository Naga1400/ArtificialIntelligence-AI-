import heapq

goal = [[1, 2, 3],
        [8, 0, 4],
        [7, 6, 5]]

moves = [(-1, 0), (1, 0), (0, -1), (0, 1)]

def find_blank(state):
    for i in range(3):
        for j in range(3):
            if state[i][j] == 0:
                return i, j

def neighbors(state):
    x, y = find_blank(state)
    result = []
    for dx, dy in moves:
        nx, ny = x + dx, y + dy
        if 0 <= nx < 3 and 0 <= ny < 3:
            new = [row[:] for row in state]
            new[x][y], new[nx][ny] = new[nx][ny], new[x][y]
            result.append(new)
    return result

def manhattan(state): # h(n)
    dist = 0
    for i in range(3):
        for j in range(3):
            v = state[i][j]
            if v != 0:
                x, y = divmod(v-1, 3)
                dist += abs(x - i) + abs(y - j)
    return dist

def astar_manhattan(start):
    frontier = [(manhattan(start), 0, start, [start])]
    seen = set()
    while frontier:
        f, g, state, path = heapq.heappop(frontier)
        if state == goal:
            return path
        t = tuple(tuple(r) for r in state)
        if t in seen:
            continue
        seen.add(t)
        for nb in neighbors(state):
            g2 = g + 1
            h2 = manhattan(nb)
            heapq.heappush(frontier, (g2 + h2, g2, nb, path + [nb]))
    return None

# Example
start = [[2, 8, 3],
         [1, 6, 4],
         [7, 0, 5]]

sol = astar_manhattan(start)
if sol:
    print("A* (Manhattan Distance) solved in", len(sol)-1, "moves")
    for s in sol:
        for r in s: print(r)
        print()
else:
    print("No solution")