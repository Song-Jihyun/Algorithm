# Merge Sort / 병합 정렬
: 분할 정복에 기반을 둔 정렬 알고리즘


## 병합정렬의 원리
<ul>
  <li><strong>Divide:</strong> 배열을 같은 크기의 두 배열로 나눈다. [O(1)]</li>
  <li><strong>Merge:</strong> 두 배열을 병합하면서 정렬한다. [O(N)]</li>
  <li><strong>Base case:</strong> 배열의 길이가 1 이하면 정렬된것으로 생각하고 return한다.</li>
</ul>
퀵 정렬도 분할 정복에 기반을 뒀지만 병합정렬과 달리 Divide 과정에서 정렬이 진행된다. 


## 시간복잡도 O(N*logN)
N개의 숫자를 정렬하기 위해서는 logN level의 binary tree가 그려진다.<br>
각 level에서는 정렬을 위해 N번의 비교 연산이 수행된다.<br>
따라서 [number of level]\*[operations per level] = N\*logN의 시간복잡도가 소요된다.<br>
<pre>
<code>
N=8

level 0: [8] // root
level 1: [4][4]                   => 8
level 2: [2][2][2][2]             => 8
level 3: [1][1][1][1][1][1][1][1] => 8

number of level = log<sub>2</sub>N
operations per level = N

Time Complexity of Merge Sort is O(N*logN)
</code>
</pre>


## mergeSort.java
<pre>
<code>
void mergeSort(int arr[], int start, int end){ <strong>//initial-> start: 0, end: arr.length</strong>
  <strong>//base case</strong>
  if(end - start <= 1) return;
		
  <strong>//divide</strong>
  int mid = (start+end) / 2;
  mergeSort(arr, start, mid);
  mergeSort(arr, mid, end);
		
  <strong>//merge</strong>
  int i = start;
  int j = mid;
		
  int temp[] = new int[end-start];
  int k = 0;
		
  while(i < mid || j < end) {
    if(i < mid && (j >= end || arr[i] <= arr[j])) {
      temp[k++] = arr[i++];
    }
    else {
      temp[k++] = arr[j++];
    }
  }
		
  for(int l=0; l < temp.length; l++) {
    arr[start+l] = temp[l];
  }
}
</code>
</pre>
