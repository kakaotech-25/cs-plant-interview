# 1. Stack

<img width="559" alt="image" src="https://github.com/user-attachments/assets/ffeb525b-ec9c-46b8-aad7-c0e7752ffaaf">


- LIFO(Last In First Out) 구조
- 가장 마지막에 저장된 데이터가 가장 먼저 삭제, 한쪽 방향에서만 데이터의 삽입과 삭제가 가능함
1. 활용사례
    - 괄호 짝 맞추기, 후위 표기법 계산 등
    - DFS, 역순 문자열 생성, 실행 취소 (undo) 등
2. 구현 방법
    
    ```python
    class Stack():
        def __init__(self):
            self.stack = []
            
        def push(self, data):
            self.stack.append(data)
            
        def pop(self):
            pop_object = None
            if self.isEmpty():
                print("Stack is Empty")
            else:
                pop_object = self.stack.pop()
                
            return pop_object
                
        def top(self):
            top_object = None
            if self.isEmpty():
                print("Stack is Empty")
            else:
                top_object = self.stack[-1]
                
            return top_object
                
                
        def isEmpty(self):
            is_empty = False
            if len(self.stack) == 0:
                is_empty = True
            return is_empty
    ```
    
    - top(peek) : 스택의 맨 위의 항목 반환
    - push : 스택 맨 위에 있는 항목을 제거하고 그 항목 반환
    - pop :  스택의 맨 위에 있는 항목을 제거하고 반환. 스택이 비어있을 경우, 에러 반환
    - isEmpty : 스택이 비어있는지 확인
    - 연결리스트, 배열로 구현가능
3. 시간 복잡도
    - 삽입, 삭제시에는 O(1), 탐색에는 O(n)의 시간복잡도를 갖는다.

# 2. Queue

- FIFO (First In First Out)
- 다른 한쪽에서는 데이터 삽입, 다른 한쪽에서는 데이터의 삭제만 가능
- 우선순위 큐, 원형 큐, 선형 큐를 가짐
1. 활용사례
    - BFS, 프린터 대기열, 버퍼관리, 스케줄링 알고리즘 등 데이터가 순차적으로 처리되어야하는 경우에 적합
    - 입출력 스트림 버퍼링도 같은 개념이다. 버퍼에 쌓아두고 앞에서부터 차례대로 접근함
2. 구현 방법
    
    ```python
    class ListQueue(object):
    	def __init__(self):
    			self.queue = []
    	
    	def dequeue(self):
    			if len(self.queue)==0:
    					return -1
    			return self.queue.pop(0)
    	
    	def enqueue(self, n):
    			self.queue.append(n)
    			pass
    		
    	def printQueue(self):
    			print(self.queue)
    ```
    
    - Enqueue : rear에서 이루어지는 삽입연산
    - Dequeue : front 에서 이루어지는 삭제 연산
    - Front :  큐의 시작 지점
    - Rear : 큐의 끝 지점
3. 종류
    1. linear queue : 데이터를 FIFO 순서로 처리하는 가장 기본적인 큐
        
        <img width="492" alt="image" src="https://github.com/user-attachments/assets/3cbb6b0c-6c3e-4d92-8612-7116e045372c">

    2. 원형 큐 : 큐의 마지막 요소가 첫 요소와 연결된 큐로, 원형으로 순환
        
        <img width="497" alt="image" src="https://github.com/user-attachments/assets/a3456a77-22f5-4106-82d8-f54431c70029">

        
    3. 우선순위 큐 : 각 데이터 요소에 우선순위를 할당하고 해당 우선순위에 따라 데이터를 처리하는 큐
        
        <img width="497" alt="image" src="https://github.com/user-attachments/assets/acf54c19-a5dd-45db-ab5b-b4bc55271261">

        
4. 시간 복잡도
    
    <img width="529" alt="image" src="https://github.com/user-attachments/assets/6161a959-ebf0-48a8-881d-d90efac4d86a">

    
    - 삽입, 삭제시에는 O(1), 탐색에는 O(n)의 시간복잡도를 갖는다.

### Deque

<img width="529" alt="image" src="https://github.com/user-attachments/assets/a4a1cc8c-cbeb-4e79-900d-432c40205c6e">


- 큐 2개를 겹쳐놓은것과 같아 Double ended Queue라고 부른다.
- 양쪽에서 데이터의 입출력이 모드 가능한 자료구조
1. 구현방법
    - JS에서는 배열의 내장메소드로 모두 구현되어있으며 스택, 큐와 마찬가지로 front와 rear라는 포인터가 있으며 이들은 각각 가장 앞, 뒤에 있는 데이터를 가르킨다.
    - 다만, 스택과 큐의 Rear는 다음 요소가 삽입 될 위치를 가르키는 반면 deque의 Rear는 마지막 요소를 가르키고 있게 됩니다.
    - python 의 경우 `from collections import deque` 를 사용하여 deque를 사용할 수 있다.
2. 시간 복잡도
    - 스택, 큐와 같이 데이터의 삽입과 삭제에 O(1)의 시간복잡도
    - python에서 list의 pop(0)은 시간복잡도가 O(n) 인데 반해, deque의 popleft는 O(1) 이기 때문에 성능 향상된다.

[참고](!https://velog.io/@moonblue/스택Stack-과-큐Queue)
