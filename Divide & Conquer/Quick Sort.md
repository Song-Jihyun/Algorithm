# Quick Sort / 퀵 정렬
: 분할 정복에 기반을 둔 정렬 알고리즘


## 퀵 정렬의 원리
<ul>
  <li><strong>Divide:</strong> 배열의 처음에 위치한 값을 기준(pivot)으로 더 작은 수와 더 큰 수를 담은 두 배열로 나눈다. [O(N)]</li>
  <li><strong>Merge:</strong> 두 배열을 병합한다. [이 과정은 생략됨]</li>
  <li><strong>Base case:</strong> 배열의 길이가 1 이하면 정렬된 것으로 생각하고 return한다.</li>
</ul>
병합 정렬도 분할 정복에 기반을 뒀지만 퀵 정렬과 달리 Merge 과정에서 정렬이 진행된다.


## 시간복잡도 O(N*logN)

### Best case: 배열이 항상 크기가 같은 두 배열로 나뉠 때
N개의 숫자를 정렬하기 위해서는 logN level의 binary tree가 그려진다.<br>
각 level에서는 정렬을 위해 N번의 비교 연산이 수행된다.<br>
따라서 [number of level]\*[operations per level] = N\*logN의 시간복잡도가 소요된다.
<pre>
<code>
N=8

level 0: [8] // root
level 1: [4][4]                   => 8
level 2: [2][2][2][2]             => 8
level 3: [1][1][1][1][1][1][1][1] => 8

number of level = log<sub>2</sub>N
operations per level = N

Time Complexity of best case is O(N*logN)
</code>
</pre>

### Worst case: 배열이 항상 1개와 나머지로 나뉠 때 (이미 정렬된 배열이 주어졌을 때)
N개의 숫자를 정렬하기 위해서는 N-1 level의 binary tree가 그려진다.<br>
각 level에서는 정렬을 위해 N-1, N-2, ..., 2, 1번의 비교 연산이 수행된다.<br>
따라서 N-1 + N-2 + ... + 2 + 1 = (N*(N-1))/2 ≈ N<sup>2</sup>의 시간복잡도가 소요된다.
<pre>
<code>
N=4

level 0: [4] // root
level 1: [1][3]       => 3
level 2: [1][1][2]    => 2
level 3: [1][1][1][1] => 1

Time Complexity of worst case is O(N<sup>2</sup>)
</code>
</pre>

### Average: 대부분의 상황에서 길이가 2 이상인 두 배열로 나뉘지만 배열간의 길이 차이가 있을 때
배열이 best case처럼 1/2 : 1/2이 아니라 1/10 : 9/10 비율로 나눠진다고 가정해보자.</br>
그럼 tree의 왼쪽 가지는 log<sub>10</sub>N의 깊이를 가지고 오른쪽 가지는 log<sub>10/9</sub>N의 깊이를 가지게 된다.<br>
또 각 level에서는 정렬을 위해 N번의 비교 연산이 수행된다.<br>
따라서 [number of level]\*[operations per level] = N\*logN의 시간복잡도가 소요된다.


## Merge Sort와 Quick Sort 사이에 차이가 생기는 이유
Merge Sort는 Divide 과정에서 무조건 절반으로 쪼개기 때문에 항상 균등 분할을 하게 된다.<br>
하지만 Quick Sort는 Divide 과정에서 피벗(pivot)으로 삼는 값이 랜덤하기 때문에 대부분의 경우 비균등하게 분할된다.<br>
이런 차이 때문에 Quick Sort는 Best case와 Worst case가 생기는 것이다.<br>
<br>
<strong>결과적으로 Merge sort는 worst case도 N*logN이기 때문에 특별한 이유가 없다면 Merge Sort를 사용하는게 유리하다.</strong>



## quickSort.java
<pre>
<code>
<strong>//Divide 과정은 배열의 큰 값과 작은 값을 교환하는 방식으로 이루어진다.</strong>

void quickSort(int arr[]) {
  quickSort(arr, 0, arr.length);
}

void quickSort(int arr[], int start, int end) {
  <strong>//base case</strong>
  if(end - start <= 1) return;
	
  <strong>//divide</strong>
  int pivot = arr[start];
  int left = start+1;
  int right = end-1;
  int temp;
		
  while(left < right) {
    while(left < end && arr[left] <= pivot) left++;
    while(right > start && arr[right] > pivot) right--;
			
    if(left < right) {
      swap(arr, left, right);
    }
  }
		
  swap(arr, start, right);
  
  quickSort(arr, start, right);
  quickSort(arr, right+1, end);
}

void swap(int arr[], int a, int b) {
  int temp;
  
  temp = arr[a];
  arr[a] = arr[b];
  arr[b] = temp;
}
</code>
</pre>
