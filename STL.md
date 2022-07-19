# Sequence Containers
> 데이터를 순차적으로 저장하는 자료구조이고, 구현이 단순해서 가볍고 빠르다.     
> 저장할 데이터가 정렬 상태를 유지할 필요가 없을 때 사용하기 좋다.

## vector(array)
> 메모리상에 데이터가 연속적으로 위치하는 배열이다.

Vector의 경우 배열의 크기를 런타임에 조절할 수 있지만(동적 할당) array는 컴파일 할 때 결정되어야 하고, 런타임에서 바꿀 수 없다.      
사용할 배열의 크기를 미리 알 수 있고, 크기가 변하지 않는다면 array, 그렇지 않다면 vector를 사용하는 것이 좋다.

### vector
> vector는 포인터 3개로 구현되어 있다.      
> 1. 할당된 배열의 시작 주소를 가리키는 포인터      
> 2. 다음에 데이터가 삽입될 위치를 가리키는 포인터      
> 3. 할당된 배열의 끝 주소를 가리키는 포인터

<img width="474" alt="image" src="https://user-images.githubusercontent.com/80378041/179690311-5f84dfde-607a-4b26-bc09-ba4ef7f4b259.png">

데이터를 뒤에 삽입하게 되면 빨간 포인터가 가리키는 곳에 삽입되고, 빨간 포인터가 1 증가하게 된다

## deque
> Container 앞, 뒤로 데이터를 빠르게 넣고 뺄 수 있는 double-ended queue이다.

deque는 여러 개의 버퍼에 데이터를 나눠서 저장한다.       
vector는 할당된 공간이 전부 차면 배열을 통째로 새로 할당하지만, deque는 버퍼 하나만 새로 할당하게 되므로, 데이터의 삽입이 언제나 O(1)이 된다.

<img width="539" alt="image" src="https://user-images.githubusercontent.com/80378041/179691092-41311df4-e72f-42ea-9dd3-f035233b4972.png">

이 상태에서 뒤에 새로운 값을 삽입하면, 버퍼 2 뒤에 버퍼 3을 새로 할당하고, 7을 넣게 된다.

## list(forward_list)
> linked list이다. Container의 어느 위치는 상수시간에 데이터를 삽입하거나 삭제할 순 있지만, index로 접근하는 random access는 불가능하다.

__list는 앞 뒤로 연결된 double linked list이고, forward_list 뒤만 저장하고 있는 singly-linked list이다.__
- singly-linked list는 Container 맨 앞에 데이터를 삽입하는 건 빠르지만, 맨 뒤에 삽입하는 것은 느리다.      
- singly-linked list는 어떤 iterator의 다음 iterator는 삭제할 수 있지만, 자신의 iterator는 삭제할 수 없다. 
- double-linked list보다 포인터를 하나 덜 가지므로 기본적인 연산이 빠르며, 메모리도 더 적게 사용하게 된다.
- double-linked list의 기능이 필요 없다면, forward_list를 사용하는게 시간과 공간 면에서 이점이 있다.

# Associative Containers
> 데이터를 정렬된 상태로 유지하는 자료구조. Red-Black Tree를 기반으로 하고 데이터의 추가, 삭제, 접근의 시간 복잡도가 모두 O(logN)이다.      
> 따라서 정렬이 굳이 필요 없다면 아래의 Unordered Associative Containers를 사용하는 게 좋다.

## set(map)
> 어떤 key를 기준으로 데이터를 저장한다. set은 데이터 자체를 key로 사용하고, map은 pair의 형태로 키를 따로 받아 사용한다.

## multiset(multimap)
> 기본적으로 set과 map은 원소의 중복을 허용하지 않는다. 하지만 multiset과 multimap은 원소의 중복을 허용하므로, 같은 key를 여러 개 저장하고 싶을 때 사용한다.     
> 하지만, 중복을 허용하므로 find나 erase를 할 때도 모든 키에 대해 동작하므로 O(logN + 중복 원소의 개수)의 시간 복잡도를 가지게 된다.

# Unordered Associative Containers
> 위에서 잠깐 말했듯이 데이터를 정렬되지 않은 형태로, 해시값을 사용해 데이터를 저장하는 자료구조이다.      
> 대부분의 경우에서 추가, 삭제, 접근이 O(1)이므로 효율적이다.

## unordered_set(unordered_map)
> 데이터를 중복없이 사용하고 싶고, 순서는 상관 없으면 set과 map 대신 사용할 수 있다.

<img width="709" alt="image" src="https://user-images.githubusercontent.com/80378041/179695229-301d2413-b603-4ec7-b2cb-e0f3eb5f9fcc.png">

unordered_map은 다음과 같은 방식으로 동작한다
1. 데이터를 여러 개의 버킷에 나누어 저장한다
2. 주어진 key의 해시값을 계산하고 이를 버킷 개수로 나눈 나머지를 구해 어떤 버킷에 들어갈지 계산한다

이 때, key와 들어가는 버킷은 상관이 없기 때문에, 해시간의 충돌때문에 각 버킷마다 linked_list로 key와 value를 저장한다.     
만약 하나의 버킷에 모든 데이터가 삽입된다면, 최악의 경우에는 추가, 삭제, 접근이 모두 O(N)이 될 수도 있다.

## unordered_multiset(unordered_multimap)
> 위의 multiset과 비슷하게 중복값을 허용한다.

# Container Adaptors
> 실제로 std library가 아닌, 컨테이너를 좀 더 편리하게 사용하도록 도와주는 interface들이다

## stack, queue
> LIFO 자료구조인 stack, FIFO 자료구조인 queue의 기능을 사용할 수 있게 해준다

## priority_queue
> 데이터가 완벽히 정렬된 상태는 아니지만, 최댓값은 빠르게 찾을 수 있는 queue이다. 데이터의 최댓값 또는 최솟값만 필요할 때 유용하게 사용할 수 있다.
