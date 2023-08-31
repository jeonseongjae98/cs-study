## DFS(깊이우선탐색)
최초 시작 정점에서 가장 먼저 이어져 있는(간선으로 연결된) 정점을 하나 찾고 해당 정점에 또 인접한 정점을 찾아 더 이상 깊이 갈 수 없을 때까지 탐색한 뒤 돌아오는 방식이다.

### DFS를 사용하는 예시
그래프의 순환이 있는지 확인하는 경우 많이 쓰인다. BFS로도 가능하지만 DFS가 더 메모리 효율적이다. 경로 찾기, 위상 정렬, 미로 찾기 등에서 사용될 수 있다.

### 구현 방법
스택 또는 재귀 방식을 이용하여 구현할 수 있다. 스택은 LIFO방식이기 때문에 인접한 정점이 우선이 아닌 더 멀리 있는(인접 정점의 끝) 정점을
우선 탐색한 뒤 돌아올 수 있다.

재귀 방식으로 진행도 가능하다. 재귀 자체가 내부적으로 Stack을 사용하기 때문이다. 둘 중에서는 재귀방식이 더 많이 쓰인다.
  
시간복잡도 : O(V+E), V는 정점 / E는 간선의 개수로 그 개수에 따라 전체 탐색에 시간이 소요된다.(인접 행렬은 O(V^2))

공간복잡도 : O(V), 최악의 경우, 정점이 1열로 이어져 전체 정점의 수 만큼 스택이 쌓일 수 있다.

### 알고리즘 동작 방식
1. 탐색 시작 노드를 스택에 삽입하고, 방문 처리한다.
2. 스택의 최상단 노드에 방문하지 않은 인접 노드가 있으면 그 인접 노드를 스택에 넣고 방문 처리하고, 방문하지 않은 인접 노드가 없으면 스택에서 최상단 노드를 꺼낸다.
3. 위의 1번과 2번 과정을 더 이상 수행할 수 없을 때까지 반복한다.

**방문 처리** : 스택에 한 번 삽입되어 처리된 노드가 다시 삽입되지 않게 체크하는 것을 의미한다. 이를 통해 각 노드를 한 번씩만 처리할 수 있다.

**예시**
 
그래프의 노드 1을 시작 노드로 설정하여 DFS를 이용해 탐색
<p align="center"><img src="https://i.postimg.cc/nLJJMLHW/img1-daumcdn.png" width="400"></p>
  
인접한 노드 중에서 방문하지 않은 노드가 여러 개 있으면 번호가 낮은 순서부터 처리한다.
방문 처리된 노드는 회색으로, 현재 처리하는 스택의 최상단 노드는 하늘색으로 표현한다.
  
**step1**. 시작 노드 ‘1’을 스택에 삽입하고 방문 처리
<p align="center"><img src="https://i.postimg.cc/D0yshFJJ/img1-daumcdn.png" width="400"></p>

**step2**. 스택의 최상단 노드 ‘1’에 방문하지 않은 인접 노드 ‘2’, ‘3’, ‘8’ 중에서 가장 작은 노드 ‘2’를 스택에 넣고 방문 처리
<p align="center"><img src="https://i.postimg.cc/MXJSRZ7X/img1-daumcdn.png" width="400"></p>

**step3**. 스택의 최상단 노드 ‘2’에 방문하지 않은 인접 노드 ‘7’을 스택에 넣고 방문 처리 
<p align="center"><img src="https://i.postimg.cc/FHWhCvmC/img1-daumcdn.png" width="400"></p>

**step4**. 스택의 최상단 노드 ‘7’에 방문하지 않은 인접 노드 ‘6’과 ‘8’ 중에서 가장 작은 노드인 ‘6’을 스택에 넣고 방문 처리
<p align="center"><img src="https://i.postimg.cc/RhRk31Zp/img1-daumcdn.png" width="400"></p>

**step5**. 스택의 최상단 노드 ‘6’에 방문하지 않은 인접 노드가 없으므로, 스택에서 ‘6’번 노드를 꺼냄
<p align="center"><img src="https://i.postimg.cc/m2gqXHDR/img1-daumcdn.png" width="400"></p>

**step6**. 스택의 최상단 노드 ‘7’에 방문하지 않은 인접 노드 ‘8’이 있으므로, ‘8’번 노드를 스택에 넣고 방문 처리 
<p align="center"><img src="https://i.postimg.cc/Hx3zX6bM/img1-daumcdn.png" width="400"></p>

**step7**. 스택 최상단 노드 ‘8’에 방문하지 않은 인접 노드가 없으므로, 스택에서 ‘8’번 노드를 꺼냄
<p align="center"><img src="https://i.postimg.cc/DzTPN9gs/img1-daumcdn.png" width="400"></p>

**step8**. 스택의 최상단 노드 ‘7’에 방문하지 않은 인접 노드가 없으므로, 스택에서 ‘7’번 노드를 꺼냄
<p align="center"><img src="https://i.postimg.cc/T24qxL0T/img1-daumcdn.png" width="400"></p>

**step9**. 스택의 최상단 노드 ‘2’에 방문하지 않은 인접 노드가 없으므로, 스택에서 ‘2’번 노드를 꺼냄
<p align="center"><img src="https://i.postimg.cc/W3D6KgKF/img1-daumcdn.png" width="400"></p>

**step10**. 스택의 최상단 노드 ‘1’에 방문하지 않은 인접 노드 ‘3’을 스택에 넣고 방문 처리
<p align="center"><img src="https://i.postimg.cc/dVtCpGZs/img1-daumcdn.png" width="400"></p>

**step11**. 스택의 최상단 노드 ‘3’에 방문하지 않은 인접 노드 ‘4’, ‘5’ 중 가장 작은 노드 ‘4’를 스택에 넣고 방문 처리
<p align="center"><img src="https://i.postimg.cc/3NFybwK0/img1-daumcdn.png" width="400"></p>

**step12**. 스택의 최상단 노드 ‘4’에 방문하지 않은 인접 노드가 없으므로, 스택에서 ‘4’번 노드를 꺼냄

**step13**. 스택의 최상단 노드 ‘3’에 방문하지 않은 인접 노드 ‘5’가 있으므로, ‘5’번 노드를 스택에 넣고 방문 처리 

**step14**. 스택의 최상단 노드 ‘5’에 방문하지 않은 인접 노드가 없으므로, 스택에서 ‘5’번 노드를 꺼냄

**step15**. 남아 있는 노드에 방문하지 않은 인접 노드가 없다. 따라서 모든 노드를 차례대로 꺼내면 다음과 같다.
<p align="center"><img src="https://i.postimg.cc/hPGPqss5/img1-daumcdn.png" width="400"></p>

- 위 단계에서 노드의 탐색 순서(스택에 들어간 순서)는 다음과 같다.
  - 1 -> 2 -> 7 -> 6 -> 8 -> 3 -> 4 -> 5
- 깊이 우선 탐색 알고리즘인 DFS는 스택 자료구조에 기초하므로, 실제 구현은 재귀 함수를 이용했을 때 간결하게 구현할 수 있다.

### 재귀를 이용한 구현
``` java
public class DFSRecursion {
    //각 노드가 방문된 정보를 1차원 배열 자료형으로 표현
    public static boolean [] visited = {false, false, false ,false ,false ,false ,false ,false, false};
    // 각 노드가 연결된 정보를 2차원 배열 자료형으로 표현
    public static int[][] graph = {{},
        {2, 3, 8},
        {1, 7},
        {1, 4, 5},
        {3, 5},
        {3, 4},
        {7},
        {2, 6, 8},
        {1, 7}};
    
    public static void main(String[] args){
        int start = 1; // 시작 노드
        dfs(start);
    }
    
    /*
	 * dfs 알고리즘을 수행하는 함수
	 * @param v 탐색할 노드
    */
    public static void dfs(int v){
        // 현재 노드 방문 처리
        visited[v] = true;
        // 방문 노드 출력
        System.out.print(v + "");
        
        // 인접 노드 탐색
        for (int i : graph[v]){
            // 방문하지 않은 인접 노드 중 가장 작은 노드를 스택에 넣기
            if (visited[i]==false){
                dfs(i);
            }
        }
    }
}
```

### Stack 클래스를 통한 DFS 구현
```java
public class DFSStack {
    public static void main(String[] args){
        
        //각 노드가 연결된 정보를 2차원 배열 자료형으로 표현
        int [][]graph = {{},
            {2, 3, 8},
            {1, 7},
            {1, 4, 5},
            {3, 5},
            {3, 4},
            {7},
            {2, 6, 8},
            {1, 7}};
        
        //각 노드가 방문된 정보를 1차원 배열 자료형으로 표현
        boolean [] visited = {false, false, false ,false ,false ,false ,false ,false, false};
        
        //정의된 DFS 함수 호출
        DFSStack dfsExam = new DFSStack();
        dfsExam.dfs(graph, 1, visited);
    }
    
    /*
     * dfs 메서드
     *  @param graph 노드 연결 정보를 저장
     *  @param v 방문을 시작하는 최상단 노드의 위치
     *  @param visited 노드 방문 정보를 저장
    */
    void dfs(int [][]graph, int start, boolean [] visited){
        //시작 노드를 방문 처리
        visited[start] = true;
        System.out.print(start + " ");//방문 노드 출력
        
        Deque<Integer> stack = new LinkedList<>();
            stack.push(start); //시작 노드를 스택에 입력
            
            while(!stack.isEmpty()){
                int now = stack.peek();
                
                boolean hasNearNode = false; // 방문하지 않은 인접 노드가 있는지 확인
                //인접한 노드를 방문하지 않았을 경우 스택에 넣고 방문처리
                for(int i: graph[now]){
                    if (!visited[i]) {
                        hasNearNode = true;
                        stack.push(i);
                        visited[i] = true;
                        System.out.print(i + " ");//방문 노드 출력
                        break;
                    }
                }
                //방문하지 않은 인접 노드가 없는 경우 해당 노드 꺼내기
                if(hasNearNode==false)
                    stack.pop();
        }
    }
}
```
### DFS와 백트래킹의 차이
DFS는 기본적으로 그래프 형태 자료구조에서 모든 정점을 탐색할 수 있는 알고리즘 중 하나이다. 깊이를 우선적으로 탐색하기에 재귀 또는 스택을 이용한다.

재귀를 이용하여 탐색을 수행한다는 부분에서 완전탐색 알고리즘의 재귀 / 백트래킹(Backtracking)과 유사한 측면이 보여 혼란이 올 수 있다.

그런데, 재귀라는 것은 말 그대로 스스로의 함수(또는 메소드)를 호출하는 방식을 의미하는 것이므로 DFS가 재귀라는 방식을 이용해 탐색을 수행하는 하나의 방식이라고 이해하면 된다.

백트래킹(Backtracking)은 재귀를 통해 알고리즘을 풀어 가는 기법 중 하나로 가지치기(Pruning)을 통해서 탐색을 시도하다가 유망하지 않으면 추가 탐색을 하지 않고 다른 해를 찾는 방법이다.

DFS는 기본적으로 모든 노드를 탐색하는 것이 목적이지만 상황에 따라서 백트래킹 기법을 혼용하여 불 필요한 탐색을 그만두는 것 또한 가능하다.

즉, DFS와 백트래킹은 유사한 부분이 있지만 기본적으로 사용 목적이 다르지만 두 기법을 혼용하여 사용하는 것이 가능하다. 완전히 다른 개념이 아니라 재귀 호출을 통한 기법 중 하나 이기 때문이다.

## BFS(너비우선탐색)
최초 시작 정점에서 가장 먼저 이어져 있는(간선으로 연결된) 정점을 모두 순회한 뒤, 각 순회된 정점부터 또 시작하여 가장 먼저 이어진 정점을 순회하는 방식을 반복한다.

### BFS를 사용하는 예시
넓이 우선 탐색은 퍼즐 게임 등의 해결 시에 굉장히 많이 쓰일 수 있다. 루빅 큐브 등의 움직임을 해결할 수 있는 방식으로 활용 될 수 있다. 또한 굉장히 유명한 다익스트라(Dijkstra) 알고리즘으로 최단 경로를 찾을 때도 활용되며 Flow Network의 Maximum Flow를 찾기 위한 Ford-Fulkerson 알고리즘에도 사용된다.

### 구현 방법
큐(Queue) 자료구조를 통해 구현된다.

### 알고리즘 동작 방식
- 선입선출 방식인 큐 자료구조를 이용하는 것이 정석이다.
   - 인접한 노드를 반복적으로 큐에 넣도록 알고리즘을 작성하면 자연스럽게 먼저 들어온 것이 먼저 나가며, 가까운 노드부터 탐색하게 된다.

1. 탐색 시작 노드를 큐에 삽입하고 방문 처리한다.
2. 큐에서 노드를 꺼내 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입하고 방문 처리한다.
3. 위의 1번과 2번 과정을 더 이상 수행할 수 없을 때까지 반복한다.

**예시**
 
그래프의 노드 1을 시작 노드로 설정하여 BFS를 이용해 탐색
<p align="center"><img src="https://i.postimg.cc/NfX6XZ5W/img1-daumcdn.png" width="400"></p>
  
인접한 노드가 여러 개 있을 때, 숫자가 작은 노드부터 먼저 큐에 삽입한다고 가정한다. 큐에 원소가 들어올 때, 위에서 들어오고 아래쪽에서 꺼낸다. 방문 처리된 노드는 회색으로, 큐에서 꺼내 현재 처리하는 노드는 하늘색으로 표시하다.
  
**step1**. 시작 노드 ‘1’을 큐에 삽입하고 방문 처리 한다.
<p align="center"><img src="https://i.postimg.cc/D0yshFJJ/img1-daumcdn.png" width="400"></p>

**step2**. 큐에서 노드 ‘1’을 꺼내고 방문하지 않은 인접 노드 ‘2’, ‘3’, ‘8’을 모두 큐에 삽입하고 방문 처리한다.
<p align="center"><img src="https://i.postimg.cc/Wb0WM53f/img1-daumcdn.png" width="400"></p>

**step3**. 큐에서 노드 ‘2’를 꺼내고 방문하지 않은 인접 노드 ‘7’을 큐에 삽입하고 방문 처리 한다. 
<p align="center"><img src="https://i.postimg.cc/wBMQb2qz/img1-daumcdn.png" width="400"></p>

**step4**. 큐에서 노드 ‘3’을 꺼내고 방문하지 않은 인접 노드 ‘4’와 ‘5’를 모두 큐에 삽입하고 방문 처리한다.
<p align="center"><img src="https://i.postimg.cc/kGsVCrsp/img1-daumcdn.png" width="400"></p>

**step5**. 큐에서 노드 ‘8’을 꺼내고 방문하지 않은 인접 노드가 없으므로 무시한다.
<p align="center"><img src="https://i.postimg.cc/pLhdG5w7/img1-daumcdn.png" width="400"></p>

**step6**. 큐에서 노드 ‘7’을 꺼내고 방문하지 않은 인접 노드 ‘6’을 큐에 삽입하고 방문 처리를 한다.
<p align="center"><img src="https://i.postimg.cc/Dymf0bwZ/img1-daumcdn.png" width="400"></p>

**step7**. 남아 있는 노드에 방문하지 않은 인접 노드가 없다. 따라서 모든 노드를 차례로 꺼낸다.
<p align="center"><img src="https://i.postimg.cc/wv6gp1r9/img1-daumcdn.png" width="400"></p>

- 위 단계에서 노드의 탐색 순서(큐에 들어간 순서)는 다음과 같다.
  - 1 -> 2 -> 3 -> 8 -> 7 -> 4 -> 5 -> 6
- 너비 우선 탐색 알고리즘인 BFS는 큐 자료구조에 기초한다.
- 구현할 때는 언어에서 제공하는 큐 라이브러리를 사용하자.
- 탐색 수행 시간은 O(N)의 시간이 소요되고, 일반적인 경우 실제 수행 시간은 DFS보다 좋다.
  - 재귀 함수로 DFS를 구현하면 컴퓨터 시스템의 동작 특성상 실제 프로그램의 수행 시간이 느려질 수 있기 때문이다.

### Queue 자료구조를 통한 DFS 구현
```java
import java.util.LinkedList;
import java.util.Queue;

public class BFS {
    public static void main(String[] args){
        //각 노드가 연결된 정보를 2차원 배열 자료형으로 표현
        int [][]graph = {{},
            {2, 3, 8},
            {1, 7},
            {1, 4, 5},
            {3, 5},
            {3, 4},
            {7},
            {2, 6, 8},
            {1, 7}};
        
        //각 노드가 방문된 정보를 1차원 배열 자료형으로 표현
        boolean [] visited = {false, false, false ,false ,false ,false ,false ,false, false};
        
        int start = 1; // 시작 노드
        // 큐 구현
        Queue<Integer> queue = new LinkedList<>();
            queue.add(start);
            
            // 현재 노드를 방문 처리
            visited[start] = true;
            
            // 큐가 빌때까지 반복
            while(!queue.isEmpty()){
                // 큐에서 하나의 원소를 뽑아 출력
                int v = queue.poll();
                System.out.println(v + " ");
                
                // 인접한 노드 중 아직 방문하지 않은 원소들을 큐에 삽입
                for (int i : graph[v]){
                    if (visited[i] == false){
                        queue.add(i);
                        visited[i] = true;
                    }
                }
            }
    }
}
```

## 문제풀이 예시
### 백준 DFS와 BFS(1260)
- 문제
  -그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오. 단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고, 더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.
- 입력
  - 첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.
- 출력
  - 첫째 줄에 DFS를 수행한 결과를, 그 다음 줄에는 BFS를 수행한 결과를 출력한다. V부터 방문된 점을 순서대로 출력하면 된다.
- 예제 입력
  - 4 5 1
  - 1 2
  - 1 3
  - 1 4
  - 2 4
  - 3 4
- 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {

	public static int[][] node;
	public static boolean[] visit;
	public static int N, M, V;
	public static StringBuilder sb = new StringBuilder();

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		N = Integer.parseInt(st.nextToken());
		M = Integer.parseInt(st.nextToken());
		V = Integer.parseInt(st.nextToken());

		node = new int[N + 1][N + 1];
		visit = new boolean[N + 1];

		for (int i = 0; i < M; i++) {
			st = new StringTokenizer(br.readLine());
			int a = Integer.parseInt(st.nextToken());
			int b = Integer.parseInt(st.nextToken());
			node[a][b] = 1;
			node[b][a] = 1;
		}

		dfs(V);
		bfs(V);
		System.out.println(sb);
	}

	public static void dfs(int v) {
		visit[v] = true;
		sb.append(v).append(" ");
		for (int i = 0; i < node[v].length; i++) {
			if (node[v][i] == 1 && !visit[i]) {
				dfs(i);
			}
		}
	}

	public static void bfs(int v) {
		Queue<Integer> queue = new LinkedList<Integer>();
		visit = new boolean[N + 1];
		visit[v] = true;
		queue.offer(v);
		sb.append("\n");
		sb.append(v).append(" ");
		while (!queue.isEmpty()) {
			int x = queue.poll();
			for (int i = 0; i < node.length; i++) {
				if (node[x][i] == 1 && !visit[i]) {
					queue.offer(i);
					visit[i] = true;
					sb.append(i).append(" ");
				}
			}
		}
	}
}
/*
1 2 4 3
1 2 3 4
*/
```
### 백준 미로탐색(2178)
- 문제
  - N×M크기의 배열로 표현되는 미로가 있다.

1	0	1	1	1	1<br>
1	0	1	0	1	0<br>
1	0	1	0	1	1<br>
1	1	1	0	1	1

  - 미로에서 1은 이동할 수 있는 칸을 나타내고, 0은 이동할 수 없는 칸을 나타낸다. 이러한 미로가 주어졌을 때, (1, 1)에서 출발하여 (N, M)의 위치로 이동할 때 지나야 하는 최소의 칸 수를 구하는 프로그램을 작성하시오. 한 칸에서 다른 칸으로 이동할 때, 서로 인접한 칸으로만 이동할 수 있다.
  - 위의 예에서는 15칸을 지나야 (N, M)의 위치로 이동할 수 있다. 칸을 셀 때에는 시작 위치와 도착 위치도 포함한다.

- 입력
  - 첫째 줄에 두 정수 N, M(2 ≤ N, M ≤ 100)이 주어진다. 다음 N개의 줄에는 M개의 정수로 미로가 주어진다. 각각의 수들은 붙어서 입력으로 주어진다.
- 출력
  - 첫째 줄에 지나야 하는 최소의 칸 수를 출력한다. 항상 도착위치로 이동할 수 있는 경우만 입력으로 주어진다.
- 예제입력
  - 4 6
  - 101111
  - 101010
  - 101011
  - 111011
- 코드
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

public class Main {

	public static int N, M;
	public static int[][] node;
	public static boolean[][] visited;
	public static int[] iDir = { -1, 0, 1, 0 };
	public static int[] jDir = { 0, 1, 0, -1 };

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());
		node = new int[N + 2][M + 2];
		visited = new boolean[N + 2][M + 2];

		String str;
		for (int i = 1; i <= N; i++) {
			str = br.readLine();
			for (int j = 1; j <= M; j++) {
				node[i][j] = str.charAt(j - 1) - '0';
			}
		}

		visited[1][1] = true;
		
		bfs(1, 1);
		
		System.out.println(node[N][M]);
		
	}

	public static void bfs(int x, int y) {
		Queue<int[]> que = new LinkedList<>();
		que.offer(new int[] { x, y });

		while(!que.isEmpty()) {
			int tmp[] = que.poll();
			int startI = tmp[0];
			int startJ = tmp[1];
			for (int i = 0; i < 4; i++) {
				int nextI = startI + iDir[i];
				int nextJ = startJ + jDir[i];
				if(!visited[nextI][nextJ] && node[nextI][nextJ] == 1) {
					visited[nextI][nextJ] = true;
					que.offer(new int[] {nextI, nextJ});
					node[nextI][nextJ] = node[startI][startJ] + 1;
				}
			}
		}
	}
}
/*
15
*/
``` 
