# Dynamic Programming / 동적 계획법
: 분할 정복과 비슷한 방식을 취하지만 중복되는 부분 문제의 답을 저장해두고 참조함으로써 문제 해결 속도를 향상시키는 알고리즘


## 동적 계획법의 예시
### 예시 1: 이항계수
이항계수 = <sub>n</sub>C<sub>r</sub> = n개의 서로 다른 원소 중에서 r개의 원소를 순서 없이 골라내는 방법의 수<br>
<sub>n</sub>C<sub>r</sub> = <sub>n-1</sub>C<sub>r-1</sub> + <sub>n-1</sub>C<sub>r</sub>의 점화식을 만족한다.
<pre>
<code>
int bino(int n, int r) {
  if(r==0 || n==r) return 1;
  return bino(n-1, r-1) + bino(n-1, r);
}
</code>
</pre>
bino(4,2) -> bino(3,1) -> <strong>bino(2,1)</strong><br>
bino(4,2) -> bino(3,2) -> <strong>bino(2,1)</strong><br>
위의 두 줄은 bino(4,2)를 구하려 했을때 그 아래로 뻗어지는 트리의 일부분을 나타낸 것인데 중간에 서로 다른 방향으로 나아갔음에도 bino(2,1)을 중복해서 호출하는 것을 볼 수 있다.<br>
이러한 중복은 트리가 깊어질수록 더 심해지기 때문에 bino(2,1)을 계산한 값을 저장해두고 그 다음부터는 bino(2,1)가 호출되었을 때 저장해둔 값을 return 해주는게 효율적이다.<br>
<pre>
<code>
int cache[][]; <strong>// main함수에서 -1로 초기화 해둔다.</strong>

int bino(int n, int r) {
  if(r==0 || n==r) return 1;
  if(cache[n][r] != -1) return cache[n][r]; <strong>// -1이 아니면 과거에 값을 계산해서 cache에 저장되어 있다는 뜻</strong>
  return <strong>cache[n][r] =</strong> bino(n-1, r-1) + bino(n-1, r);
}
</code>
</pre>


## 시간복잡도
(존재하는 부분 문제의 수) * (한 부분 문제의 시간복잡도)
