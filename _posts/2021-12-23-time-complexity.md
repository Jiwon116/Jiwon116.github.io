---
title:  "알고리즘의 시간 복잡도 분석"
# excerpt: "서브제목"

categories:
  - algorithm-concept
tags:
  - [알고리즘, 시간복잡도]

toc: true
toc_sticky: true
 
date: 2021-12-23
last_modified_at: 2021-12-23
---
📢 해당 포스팅은 **『알고리즘 문제해결 전략 1권』 (구종만 저) - '4장 알고리즘의 시간 복잡도 분석'**을 바탕으로 작성했습니다. 
{: .notice--primary}

## 시간복잡도란?
우리가 작성한 코드는 실행시간이 얼마나 걸릴까?
실행해보기 전에 정확한 시간을 추측하는 것은 힘들겠지만 반복문을 몇 번 사용했는지, 입력값은 어떻게 되는지 등을 통해 대략적으로 이 정도 되겠구나.. 를 추측할 수 있다. 즉, 우리는 **입력값과 연산 수행 시간의 상관관계를 나타내는 척도**를 `시간 복잡도 (time complexity)`라고 한다.

## Big-O 표기법이란?
같은 알고리즘을 가지고 테스트를 하더라도 <u>입력 값이 달라짐에 따라</u> 수행 시간은 매우 짧아질 수도, 매우 길어질 수도 있다. 만약, 1부터 10까지 오름차순으로 정렬을 하고자 한다.

![image](https://user-images.githubusercontent.com/63892688/147265010-960afd47-cf01-4512-a48b-eb42698f2268.png)

위와 같은 순서로 배열에 입력 값이 들어가 있다면, 2와 1을 바꾸면 정렬은 끝난다.

![image](https://user-images.githubusercontent.com/63892688/147265253-c3bddb13-995d-4b66-988b-95a312b89ea2.png)

하지만 위의 순서라면, 10부터 1까지 전부 바꿔야 한다.

이처럼, 최악의 상황일 때 걸리는 시간을 표현한 것이 `Big-O 표기법 (Big-O notation)`이다.


## 반복문의 중요성
대부분의 알고리즘 수행 시간은 **반복문**이 지배하고 있다. 즉, ```알고리즘 수행 시간 ≒ 반복문이 수행되는 횟수``` 라는 것이다.
```c++
// 주어진 배열 A에서 가장 많이 등장하는 숫자를 반환한다.
// 만약 두가지 이상 있을 경우, 아무거나 반환한다.

int majority1(const vector<int>& A) {
    int N = A.size();
    int majority = -1, majorityCount = 0;
    
    for (int i = 0; i < N; ++i) {
        // A에 등장하는 A[i]의 수를 센다.
        int V = A[i], count = 0;
        for(int j = 0; j < N; ++j) {
            if(A[j] == V) {
                ++count;
            }
        }
        
        // 지금까지 본 최대 빈도보다 많이 출현하면 답을 갱신한다.
        if (count > majorityCount) {
            majorityCount = count;
            majority = V;
        }
    }

    return majority;
}
```
배열의 크기를 N이라고 하면, 위의 코드의 수행 시간은 배열의 크기 N에 따라 달라진다. 반복문이 두 개 겹쳐져 있기 때문에, 반복문의 가장 안쪽은 항상 \\(N^2\\)번 실행된다. 따라서, 위의 코드의 수행 시간은 \\(O(N^2)\\)이 된다.


## 대표적인 알고리즘 수행 시간
### 선형 시간 알고리즘
`선형 시간(linear time) 알고리즘`이란, 수행 시간이 입력 크기 N에 정비례하는 알고리즘을 말한다. 선형 시간 알고리즘은 이름에서 알 수 있듯이, 입력 크기에 대비해 걸리는 시간을 그래프로 그리면 정확히 직선이 된다. 주어진 입력을 한 번씩 보기만 해도 선형 시간이 걸릴 수 밖에 없기 때문에, 우리가 <u>찾을 수 있는 가장 좋은 알고리즘</u>인 경우가 많다.

### 선형 이하 시간 알고리즘
어떤 문제든 입력된 자료를 최소한 한 번씩 보는 시간(선형 시간)은 반드시 필요하다. 그런데 `선형 이하 시간 알고리즘`이라니? 존재하지 않을 것 같지만, 예시를 보면 간단하게 이해할 수 있다.

<center><img src="https://user-images.githubusercontent.com/63892688/147254417-eafd4989-b005-4948-be2c-04b158d3cb22.png" width="500" height="600"> </center>

**이진 탐색(binary search)**의 경우, 찾고자 하는 값이 중간 값보다 크고 작음을 통해 입력된 자료를 절반으로 나눠서 탐색한다. 매번 절반씩 나눠서 입력된 자료를 보기 때문에, 밑이 2인 로그 \\(log_2\\)로 수행 시간을 나타낸다. (간단하게 \\(lg\\)라고 줄여쓴다.)

### 지수 시간 알고리즘
`다항 시간 알고리즘`이란, (제일 위에서 언급한 것과 같이) 반복문의 수행 횟수를 입력 크기의 다항식으로 표현할 수 있는 알고리즘을 뜻한다. \\(N^2\\)도, \\(N^{100}\\)도 모두 다항 시간이라고 묶어서 말하기 때문에, 다항 시간 알고리즘 간에는 엄청난 시간 차이가 있을 수 있다.

다항 시간보다 더 오랜 시간이 걸리는 알고리즘이 바로 `지수 시간 알고리즘`이다. 

```c++
// 음식 메뉴 정하기

const int INF = 987654321;

// 이 메뉴로 모두가 식사할 수 있는지 여부를 반환한다.
bool canEverybodyEat(const vector<int>& menu);

// 요리할 수 있는 음식의 종류 수
int M;

// food번째 음식을 만들지 여부를 결정한다.
int selectMenu(vector<int>& menu, int food) {
    // 모든 음식에 대해 만들지 여부를 결정했을 때
    if (food = M) {
        if (canEverybodyEat(menu)) return menu.size();
        
        // 아무것도 못 먹는 사람이 있으면 아주 큰 값을 반환한다.
        return INF;
    }

    // 이 음식을 만들지 않는 경우의 수를 계산한다.
    int ret = selectMenu(menu, food + 1);

    // 이 음식을 만드는 경우의 수를 계산해서 더 작은 것을 취한다.
    menu.push_bcck(food);
    ret = min(ret, selectMenu(menu, food + 1));
    menu.pop_back();
    return ret;
}
```
위의 코드는 모든 답을 한 번씩 다 확인하기 때문에, 전체 수행 시간은

(canEverybodyEat()의 수행 시간) * (M가지의 음식마다 만들지, 안 만들지 결정하는 선택지) = \\(N * M * 2^m\\)

가 된다. 이와 같이, N이 하나 증가할 때마다 걸리는 시간이 배로 증가하는 알고리즘들을 지수 시간(exponential time)에 동작한다고 말한다. 지수 시간은 <u>가장 큰 수행 시간 중 하나</u>로, 입력의 크기에 따라서 다항 시간과는 비교도 안되게 빠르게 증가한다.

## 시간복잡도 정리

|**알고리즘**|시간복잡도(Big-O)|
|:---:|:---:|
|상수 시간|O(1)|
|선형 이하 시간|O(lgN)|
|선형 시간|O(N)|
|다항 시간|O(N ^ 반복문 횟수)|
|지수 시간|O(2 ^ N)|

<br>
<center><img src="https://user-images.githubusercontent.com/63892688/147258985-946f2ac1-535b-43d8-94a9-3e475368c06e.png" width="600" height="350"> </center>

<br>
<center><img src="https://user-images.githubusercontent.com/63892688/147263032-9f4b993e-3422-4579-9562-700350ab84b2.png" width="600" height="250"> </center>

<br>

🙌 **참고 자료** 🙌 <br><br>
Big-O 표기법 (<https://todaycode.tistory.com/45>) <br>
이진탐색 (<https://minhamina.tistory.com/127>) <br>
시간복잡도 그래프 (<https://www.bigocheatsheet.com/>) <br>
시간복잡도에 따른 예시 (<https://jocoma.tistory.com/entry/%EC%8B%9C%EA%B0%84-%EB%B3%B5%EC%9E%A1%EB%8F%84-%EA%B3%B5%EA%B0%84-%EB%B3%B5%EC%9E%A1%EB%8F%84>)
{: .notice}