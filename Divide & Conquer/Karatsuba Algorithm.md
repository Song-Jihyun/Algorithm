# Karatsuba Algorithm / 카라츠바 알고리즘
: 자료형에 담을 수 없는 아주 큰 두 수를 곱하는 알고리즘


## multiply.java
일반적인 방법을 사용하면 전체 숫자 쌍을 한번식 곱해야 하기 때문에 O(N<sup>2</sup>)의 시간복잡도가 소요된다.
<pre>
<code>
int[] multiply(int[] a, int[] b) {
  int ret[] = new int[a.length + b.length];
  for(int i=0; i&lta.length; i++) {
    for(int j=0; j&ltb.length; j++) {
      ret[i+j+1] += a[i] * b[j];
    }
  }
		
  //normalize
  for(int i=ret.length-1; i>0; i--) {
    ret[i-1] += ret[i]/10;
    ret[i] = ret[i]%10;
  }
		
  return ret;
}
</code>
</pre>


## 카라츠바 알고리즘의 원리
카라츠바 알고리즘은 두 수를 각각 절반으로 쪼개면서 시작한다. 여기서는 두 수 a와 b가 각각 256자리 수라고 가정하도록 한다.
<ul>
  <li>a = a<sub>1</sub> * 10<sup>128</sup> + a<sub>0</sub><br>
      b = b<sub>1</sub> * 10<sup>128</sup> + b<sub>0</sub></li>
  <li>a * b = (a<sub>1</sub> * 10<sup>128</sup> + a<sub>0</sub>) * (b<sub>1</sub> * 10<sup>128</sup> + b<sub>0</sub>)<br>
      　　&nbsp;= a<sub>1</sub> * b<sub>1</sub> * 10<sup>256</sup> + (a<sub>1</sub> * b<sub>0</sub> + a<sub>0</sub> * b<sub>1</sub>) * 10<sup>128</sup> + a<sub>0</sub> * b<sub>0</sub></li>
  <li>z<sub>0</sub> = a<sub>1</sub> * b<sub>1</sub><br>
      z<sub>1</sub> = a<sub>1</sub> * b<sub>0</sub> + a<sub>0</sub> * b<sub>1</sub><br>
      z<sub>2</sub> = a<sub>0</sub> * b<sub>0</sub><br>
      <strong>곱셈 네 번 필요</strong></li>
  <li>(a<sub>0</sub> + a<sub>1</sub>) * (b<sub>0</sub> + b<sub>1</sub>) = (a<sub>0</sub> * b<sub>0</sub>) + (a<sub>1</sub> * b<sub>0</sub> + a<sub>0</sub> * b<sub>1</sub>) + (a<sub>1</sub> * b<sub>1</sub>)<br>
      　　　　　　　　&nbsp;&nbsp;= z<sub>2</sub> + z<sub>1</sub> + z<sub>0</sub></li>
  <li>z<sub>0</sub> = a<sub>1</sub> * b<sub>1</sub><br>
      z<sub>1</sub> = (a<sub>0</sub> + a<sub>1</sub>) * (b<sub>0</sub> + b<sub>1</sub>) - z<sub>0</sub> - z<sub>2</sub><br>
      z<sub>2</sub> = a<sub>0</sub> * b<sub>0</sub><br>
      <strong>곱셈 세 번 필요</strong></li>
</ul>


## 시간복잡도 O(N<sup>log3</sup>)


## karatsuba.java
