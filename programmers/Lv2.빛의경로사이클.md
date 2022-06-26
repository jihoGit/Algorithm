# 빛의 경로 사이클 (구현/시뮬레이션)

- 문제 출처 : https://programmers.co.kr/learn/courses/30/lessons/86052?language=python3

&nbsp;

## 1. 설계

- 입력 : 격자 정보 SL, LR (500*500)
- 출력 : 격자를 통해 만들어지는 빛의 경로 사이클의 모든 길이 오름차순
- 조건 : 
    - s : 직진
    - l : 좌회전
    - r : 우회전
    - 격자 끝을 넘어갈 경우 반대쪽 끝으로 다시 돌아옴

&nbsp;
1. 모든 노드, 모든 방향에 대해 조사
2. 탐색을 진행하면서 중간에 시작 노드가 아니고 이미 방문한 노드를 만나면 return 0
3. 시작노드를 만나면 return cnt
4. cnt를 받아서 answer 배열에 추가
5. answer 배열 오름차순 정렬

&nbsp;

## 2. 풀이

```python
def check(x, y, d) :
    # 상우하좌
    dx = [-1, 0, 1, 0]
    dy = [0, 1, 0, -1]
    
    origin = [x, y, d]
    visited[x][y][d] = True
    cnt = 0
    
    while True :
        x = (x + dx[d]) % n
        y = (y + dy[d]) % m
        if graph[x][y] == 'R' :
            d = (d+1) % 4
        elif graph[x][y] == 'L' :
            d = (d-1) % 4
        
        cnt += 1
        
        if visited[x][y][d] == True :
            if origin == [x, y, d] :
                return cnt
            else :
                return 0
        
        visited[x][y][d] = True
    
    
def solution(grid):
    global n, m, graph, visited
    graph = grid
    n = len(grid)
    m = len(grid[0])
    visited = [[[False]*4 for _ in range(m)] for _ in range(n)]
    # print("n, m = ", n, m)
    
    answer = []
    
    for x in range(len(grid)) :
        for y in range(len(grid[0])) :
            for d in range(4) :
                if visited[x][y][d] == False :
                    cnt = check(x, y, d)
                    if cnt != 0 :
                        answer.append(cnt)
                    
    return sorted(answer)
```

&nbsp;
## 3. 개선할 점

1. 문제에 대한 이해 부족
    - 사이클에 대한 개념이 부족하였다. (모든 노드를 방문해야하는 줄 알았음)
        - 사이클(cycle): 단순 경로의 시작 정점과 종료 정점이 동일한 경우
            - 단순 경로(Simple Path): 경로 중에서 반복되는 정점이 없는 경우
&nbsp;

    - 입출력 예2, 3을 보면 같은좌표, 같은 방향으로 들어와야 사이클이 성립한다는 것을 알 수 있다. -> 방향까지 저장해야함

    - 특정노드에서 빛이 이동하는 경우에 그 중간에서 거쳐진 노드들은 중복해서 조사할 필요가 없다. (결국 겹침)

&nbsp;

# 4. 총평 
- 구현, 시뮬레이션 문제 열심히 연습해서 문제 파악 및 설계 시간을 줄이고 전체적인 시간을 단축해야겠다.