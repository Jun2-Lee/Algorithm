# SCC(Strongly Connected Component)
---
> 강결합 컴포넌트란 방향성 그래프에서 다음 조건을 만족하는 정점들의 집합을 말한다.     
> 1. SCC 내의 임의의 두 정점 u,v 사이에서 u -> v도 갈 수 있고, v -> u도 갈 수 있어야 한다.     
> 2. SCC 내의 임의의 점 u와, SCC 외부의 임의의 점 v 사이에, u -> v, v -> u로 갈 수 있는 경로가 없어야 한다.     
> 
> 즉, SCC는 내부의 모든 정점에서 다른 내부의 모든 정점으로 갈 수 있는 최대 그룹이다.      
> 이 SCC는 임의의 그래프 G 안에 여러개가 존재할 수도있다.      
> 또한, 임의의 그래프 G 전체가 SCC일 수도 있는데, 이 때는 Strongly Connected Digraph라고 한다.      

![image](https://user-images.githubusercontent.com/80378041/172870602-e3880826-4929-4008-8cc4-79a205e73803.png)     
위의 그래프를 예로 들자면, {1,2,4}, {5,6}, {3} 으로 3개의 SCC가 존재하는 것이다.

## Kosaraju's algorithm
> 위에서 설명한 SCC를 구하기 위한 하나의 알고리즘이다.     
> 순서는 다음과 같다.

### 1. 그래프 G에서 DFS를 하며 각 정점의 Finish Time을 저장한다.
> 위의 그래프를 예시로 들면, 다음과 같은 트리로 나타낼 수 있다.

![image](https://user-images.githubusercontent.com/80378041/172871290-d0074a78-5e03-46d2-8585-3439f918dcea.png)
> 여기서 discovery time은 그 정점을 처음 방문한 시간이고, Finish time은 그 자식 노드들을 전부 방문하고 난 뒤 나온 시간을 말한다.

### 2. 그래프 G에서 모든 간선의 방향을 반대로 바꾼 역방향 그래프 T를 만든다.
> 위의 그래프를 역방향으로 그려주면, 다음과 같이 만들어진다.

![image](https://user-images.githubusercontent.com/80378041/172871766-42a5e11b-7d72-4439-95f9-733e44c12243.png)     

### 3. Finish Time이 큰 정점부터, 즉 늦게 끝난 정점부터 역방향 그래프 T에서 DFS를 한다. 이 때 생기는 DFS 트리들이 각각 하나의 SCC들이 된다.
![image](https://user-images.githubusercontent.com/80378041/172872054-a0436e46-cf49-4465-b279-6c4081d2badd.png)

- 1번 정점의 finish time이 가장 크기 때문에, 1번 정점부터 그래프 T에서 DFS를 한다. 4번 정점에서는 시작점인 1번으로 갈 수 없기 때문에 1 - 2 - 4에서 트리가 끝나게 된다.
- 아직 방문하지 않은 3,5,6번 정점중에 finish time이 가장 큰 5번 정점부터 다시 시작하게 되면, 6번을 방문한 뒤 갈곳이 없어지고, 5 - 6에서 트리가 끝나게 된다.
- 나머지 3번 정점이 마지막 트리가 된다.
- 이렇게 생긴 DFS 트리들이 각각 SCC가 된다.
