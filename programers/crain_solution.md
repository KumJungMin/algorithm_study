# 1. 크레인 인형뽑기 게임

## 1) 문제

### (1) 문제 정보 
 - 2019 카카오 개발자 겨울 인턴십 문제
 
 - LEVEL1
 
 - <a href="https://programmers.co.kr/learn/courses/30/lessons/64061?language=python3">문제보러가기</a>
 
 <br/>

### (2) 문제 설명

: 크레인 인형뽑기는 N x N 크기의 정사각 격자이며 위쪽에는 크레인이 있고 오른쪽에는 바구니가 있습니다.

: 각 격자 칸에는 다양한 인형이 들어 있으며 인형이 없는 칸은 빈칸입니다. 

: 모든 인형은 1 x 1 크기의 격자 한 칸을 차지하며 격자의 가장 아래 칸부터 차곡차곡 쌓여 있습니다. 

: 게임 사용자는 가장 위에 있는 인형을 집어 올리고 이 인형으 바구니에 넣습니다.
 
: 이때 바구니의 가장 아래 칸부터 인형이 순서대로 쌓이게 됩니다. 

다음 그림은 [1번, 5번, 3번] 위치에서 순서대로 인형을 집어 올려 바구니에 담은 모습입니다.

<img src="https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/638e2162-b1e4-4bbb-b0d7-62d31e97d75c/crane_game_102.png"/>

만약 같은 모양의 인형 두 개가 바구니에 연속해서 쌓이게 되면 두 인형은 터뜨려지면서 바구니에서 사라지게 됩니다. 

위 상태에서 이어서 [5번] 위치에서 인형을 집어 바구니에 쌓으면 같은 모양 인형 두 개가 없어집니다.

<img src="https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/8569d736-091e-4771-b2d3-7a6e95a20c22/crane_game_103.gif"/>

- 입출력 예

board | moves | result
---- | ---- | ----
[[0,0,0,0,0],[0,0,1,0,3],[0,2,5,0,1],[4,2,4,4,2],[3,5,1,3,1]] | [1,5,3,5,1,2,1,4] | 4

<br/>

## 2) 풀이

*이 문제는 큐, 스택 문제입니다.*

### (1) 내가 사용한 해결 

정확성 | 연산시간 | 메모리 
---- | ---- | ----
100% | 0.03ms~0.96ms | 10.2MB

a. 입력값 borad의 정렬을 변경하여 box라는 새로운 배열을 만든다.
```
  1,2,3,4,5번
[[0,0,0,0,0],           1번 [0,0,0,4,3]
 [0,0,1,0,3],           2번 [0,0,2,2,5]
 [0,2,5,0,1],   ->      3번 [0,1,5,4,1]
 [4,2,4,4,2],           4번 [0,0,0,4,3]
 [3,5,1,3,1]]           5번 [0,3,1,2,1]
```

b. moves의 원소수만큼 반복한다.

c. 만약 크레인이 접근한 번호에서, 맨 위의 값이 0이 아니면 해당 값을 pop하고 결과바구니에 담는다.

d. 만약 결과 바구니(result)에서 제일 마지막에 위치한 연속된 두 값이 같으면 answer+2를 하고 pop()을 2번 실행한다.

```python
def solution(board, moves):
    box = makeBorad(board)        #a
    answer = 0
    result = []                   #바구니
  
    for item in moves:            #b
        if(len(box[item-1]) > 0): #c
            num = box[item-1].pop(0)
            result.append(num)
            
        if((len(result)>1) and (result[len(result)-2] == result[len(result)-1])):  #d
            answer = answer + 2;
            result.pop(len(result)-2)
            result.pop(len(result)-1)
                   
    return answer;    
    
    
def makeBorad(arr):
    boxs = [[] for _ in range(len(arr))]     #2차원배열 초기화
    for i in range(0, len(arr)):
        for j in range(0, len(arr)):   
            if(arr[i][j] != 0):
                boxs[j].append(arr[i][j])
    return boxs;
```

<br/>

### (2) 대다수가 사용한 해결방법

정확성 | 연산시간 | 메모리 
---- | ---- | ----
100% | 0.03ms~1.15ms | 10.2MB

a. 작은 입력값 위주로 문제풀이를 하였다.

b. 입력값을 그대로 유지하였다.

c. 특정 조건일때만 추가하고 다음 입력값으로 넘어가는 경우 break를 이용하였다.

```python
def solution(board, moves):  
    stacklist = []
    answer = 0

    for i in moves:                  #a
        for j in range(len(board)):  #b
            if board[j][i-1] != 0:
                stacklist.append(board[j][i-1])
                board[j][i-1] = 0

                if len(stacklist) > 1:
                    if stacklist[-1] == stacklist[-2]:
                        stacklist.pop(-1)
                        stacklist.pop(-1)
                        answer += 2     
                break                 #c

    return answer
```
