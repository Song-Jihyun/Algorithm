# Recursive Function / 재귀 함수
: 자기 자신을 반복적으로 호출하는 함수


## 재귀함수의 예시
예시 1: 숫자 N이 주어졌을 때 1~N까지 숫자의 합을 구하는 함수
<pre>
<code>
int sum(int N){
  if(N == 1) return 1; <strong>// base case</strong>
  
  return N + sum(N-1);
}
</code>
</pre>

예시 2: 1~N까지 숫자가 쓰여있는 N개의 숫자 카드 중 [selectNum]개를 고르는 모든 경우의 수를 출력
<pre>
<code>
void selectCard(Stack&ltInteger&gt selected, int selectNum, int N) {
  if(selectNum == 0){ <strong>// base case</strong>
    [Stack에 있는 값 출력]
    return;
  }
  
  int init = selected.empty() ? 1 : selected.peek() + 1;
  for(int i=init; i<=N; i++) {
    selected.push(i);
    selectCard(selected, selectNum - 1, N);
    selected.pop();
  }
}
</code>
</pre>


## Base Case / 기저 사례
재귀 호출을 종료하는 단계로 결과를 출력하거나 상수값을 return한다.<br>
재귀 함수는 [하나의 큰 작업]을 [반복되는 작은 작업 + 나머지 작업]으로 조각내면서 처리해나가는데, 더이상 함수에 주어진 작업을 조각낼 수 없을 때 base case가 호출된다.
<ul>
  <li>예시 1: [1~N의 합을 구하기]를 [N + 1~N-1의 합 구하기]으로 쪼개는데 1~1의 합은 더이상 쪼갤 수 없기 때문에 N==1을 base case로 설정</li>
  <li>예시 2: [카드 4장 고르기]를 [카드 1장 고르기 + 카드 3장 고르기]로 쪼개는데 골라야 하는 카드가 한장 남은 남은 상황은 더이상 쪼갤 수 없기 때문에 selectNum==0을 base case로 설정</li>
</ul>


## 수학적 귀납법
P(1)이 참이고 P(N) -> P(N+1)이 참이면 모든 자연수 N에 대하여 P(N)은 참이다.


## 시간복잡도
가능한 모든 경우의 수
<ul>
  <li>예시 1: O(N)</li>
  <li>예시 2: O(<sub>N</sub>P<sub>selectedNum</sub>)</li>
</ul>


## Solution Link
<ul>
  <li>https://github.com/Song-Jihyun/Solution/blob/master/Algospot_BOGGLE.java</li>
  <li>https://github.com/Song-Jihyun/Solution/blob/master/Algospot_PICNIC.java</li>
</ul>
