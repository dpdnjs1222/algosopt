https://algospot.com/judge/problem/read/ALLERGY


### NP완비


__ 11.9 알러지 문제를 해결하는 첫 번째 조합 탐색 알고리즘__

```c++

int n, m;

//eaters[food] = food를 먹을 수 있는 친구들의 번호
vector<int> eaters[50];
int best;
//food : 이번에 고려해야할 음식의 번호
//edible : 지금까지 고른 음식 중 i번 친구가 먹을 수 있는 음식의 수
//chosen : 지금까지 고른 음식의 수

void slowSearch(int food, vector<int>& edible, int chosen){

	//간단한 가지치기
	if(chosen >= best) return;

	//기저사례 : 모든 음식에 대해 만들지 여부를 결정했으면,
	//모든 친구가 음식을 먹을 수 있는지 확인하고 그렇다면 최적해를 갱신한다.
	if(food == m){
		if(find(edible.begin(), edible.end(), 0) == edible.end())
			best = chosen;
		return;
	}


	//food를 만들지 않는 경우
	slowSearch(food + 1, edible, chosen);

	//food를 만드는 경우
	for(int i = 0; i < eaters[food].size(); i++){
		edible[eaters[food][j]]++;
	}

	slowSearch(food + 1, edible, chosen + 1);

}


```


<pre>
	Q. 이 코드에서 탐색을 하는 방법에 대해 그림으로 설명해봅시다.
	   왜 NP완비 문제인 걸까요?
	   
	Q. 이 코드에서 좀 더 최적화하는 방법은 무엇이 더 있을까요?


</pre>


### Q. 이 코드에서 좀 더 최적화하는 방법은 무엇이 더 있을까요?




