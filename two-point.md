# Two Pointer
---
> 투 포인터 알고리즘 또는 슬라이딩 윈도우라고 부른다.     
> 이름 그대로 두개의 포인터를 조작하며 원하는 조건을 만족하는 요소를 찾는 방법이다.

예를 들어, N개의 1차원 배열이 있을 때, 원소의 합이 정확하게 5가 되는 경우의 구간을 모두 구하는 경우이다.      
<img width="660" alt="image" src="https://user-images.githubusercontent.com/80378041/177042458-41368ce7-8eb1-4237-83ef-9da95a8f9fd6.png">     
위의 경우가 초기 상태이다. 빨간 화살표는 구간의 시작점, 파란 화살표는 구간의 끝을 가리킨다.

<img width="660" alt="image" src="https://user-images.githubusercontent.com/80378041/177042502-6204660c-1e9a-4eaa-af11-bf4d323da4ff.png">     
end가 뒤로 움직일 때는 새로운 원소를 더하고, start가 움직일 때는 그 원소를 빼는 방법으로 구간의 합을 쉽게 구할 수 있다.

<img width="666" alt="image" src="https://user-images.githubusercontent.com/80378041/177042577-7e55c89f-4a8a-4acd-988d-ab5629ce64af.png">     
end가 계속 증가해 결국 합이 5를 넘어가게 되면, 조건을 넘어버렸으므로 start를 움직이게 된다.

<img width="658" alt="image" src="https://user-images.githubusercontent.com/80378041/177042662-f33920b8-3527-4d8d-acd5-2a3d59c2f862.png">     
start를 한칸 움직였을 때, 합이 5가 되었으므로 조건을 만족하는 구간을 하나 찾았다.      
그 뒤에 start를 하나 더 움직여주고, 다시 초기상태로 돌아간 것 처럼 end부터 움직여 모든 구간을 찾는 방법이 바로 투 포인터 방식이다.


마지막에 결국 end가 배열 전체의 끝을 가리키게 되었지만, 구간의 합이 5를 넘지 못했으면, 바로 loop를 종료시키면 되고,     
합이 5를 넘었으면, start를 움직여 조건을 만족하는 구간이 더 남았는지 확인하면 모든 탐색이 끝나게 된다.


#### 이 알고리즘의 시간 복잡도는 O(N)이 되게 되는데, 매 루프마다 두 포인터중에 하나는 1씩 증가하고 있고,        
#### 각 포인터가 최대 N번씩 증가하게 되고, N + N으로 2N이 되어서, 결국 O(N)이 된다.





