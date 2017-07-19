https://algospot.com/judge/problem/read/BOARDCOVER2


## 문제 요구 사항 파악
<pre>
이 문제를 모두 풀어보셨나요?
이 문제를 보고 나서 아 우선 완전 탐색을 해야겠구나라고 생각했으면 좋은 접근 순서입니다.
그런데 어떻게 완전 탐색을 하면 될지 머릿속에서는 떠올랐을텐데 막상 구현하려니 
뭘 어떻게 뭐부터 해야할지 헷갈리 셨을 것 입니다.

네 그렇습니다. 이 문제는 조합탐색의 가지치는 좋은 문제인 것 같지 않아요.
구현이 어려운 문제입니다.

하지만, 책에선 간단하게 가지치는 방법에 대해 소개하고 있습니다.
혹시 완전탐색의 탐색 범위를 이런 방법으로 줄여보았다라고 하는 분 있으면 말해봅시당.
 



이 문제를 책을 안보고 풀기에는 힘들었을 것입니다.
왜냐하면 구현해야할 요구사항이 많기 때문입니다.

구현 요구사항들이 무엇들이 있었는지 한 번 말해볼까용?
</pre>



###전처리
<pre>

우선 입력받은 블록을 어떻게 처리하면 좋을까요?



회전을 한 것을 왜 미리 모아두는지 말해봅시다.
</pre>


코드 11.7 블록의 회전된 형태를 계산하고 상대좌표의 목록으로 변환하기<br/>  
```c 
//블록의 각 회전된 형태를 상대 좌표의 목록으로 저장해둔다.
vector<vector<pair<int, int> > > rotations;
//블록의 크기
int blockSize;
//2차원 배열 arr을 시계방향으로 90도 돌린 결과를 반환한다.
vector<string> rotate(const vector<string>& arr){
	vector<string> ret(arr[0].size(), string(arr.size(), ' '));
	for(int i = 0; i < arr.size(); i++){
		for(int j = 0; j < arr[0].size(); j++){
			ret[j][arr.size() - i - 1] = arr[i][j];
	return ret;
}

```
<pre>

Q. rotations을 pair<int, int>로 저장한 이유는 무엇입니까?

Q. 90도 회전하는 공식은 왜 저렇게 나오는 걸까요?


</pre>


코드 11.7 블록의 회전된 형태를 계산하고 상대좌표의 목록으로 변환하기<br/>  

```c

//block의 네가지 회전 형태를 만들고 이들의 상대 좌표릐 목록으로 변환한다.
void generateRotations(vector<string> block){
	rotations.clear();
	rotations.resize(4);
	for(int rot = 0; rot < 4; rot++){
		int originY = -1; int originX = -1;
		for(int i = 0; i < block.size(); i++)
			for(int j = 0; j < block[i].size(); j++)
				if(block[i][j] == '#'){
					if(originY == -1){
						//가장 윗줄 맨 왼쪽에 있는 칸이 '원점'이 된다.
						originY = i;
						originX = j;
					}
					//각 칸의 위치를 원점으로부터의 상대좌표로 표현한다.
					rotations[rot].push_back(make_pair(i - originY, j - originX));
				}
			//블록을 시계 방향으로 90도 회전한다.
			block = rotate(block);
		}
	
	//네 가지 회전 형태 중 중복이 있을 경우 이를 제거한다.
	sort(rotations.begin(), rotations.end());
	rotations.erase(unique(rotations.begin(), rotations.end()), rotations.end());
	//블록이 몇 칸 짜리인지 저장해 둔다.
	blockSize = rotations[0].size();
}
				

```

<pre>
Q. 그림 11.8의 4가지 회전에서 번호를 메겨볼까요?

Q. 왜 블록의 가장 맨 위 가장 맨 왼쪽 것이 0,0이 되었을까요?

</pre>



## 완전탐색
