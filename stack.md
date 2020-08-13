# 2. 스택

## 1) 스택이란?

: 후입선출(Last In First Out)으로, 나중에 들어간 게 먼저 나오는 구조이다.

: 스택에는 2개의 종단점(top, base)이 있는데, 가장 최근은 top, 가장 오래된 것은 base에 위치한다.

<br/>

## 2) 스택 만들기

: 스택을 나타내는 클래스를 직접 작성할 수 있다.

### (1) 스택 구현시 필수 메소드

- push(원소(들)) : 스택 꼭대기에 새 원소를 추가한다.

- pop() : 스택 꼭대기 원소를 반환하고, 해당 원소를 삭제한다.

- peek() : 스택 꼭대기 원소를 반환하지만, 해당 원소를 삭제하지 않는다.(참조역할)

- isEmpty() : 스택에 원소가 하나도 없으면 true, 스택의 크기 > 0 이면 false를 반환한다.

- clear() : 스택의 모든 원소를 삭제한다.

- size() : 스택의 원소 개수를 반환한다.

<br/>

### (2) push()

- push()는 스택에 새로운 원소르 추가하는 메소드이다.

- 단, 스택의 top에마 원소를 넣을 수 있다.

```javascript
this.push = function(element){
  items.push(element);
}
```

<br/>

### (3) pop()

- 가장 마지막에 추가한 원소를 먼저 삭제한다.

```javascript
this.pop = function(){
  return items.pop();
}
```

<br/>

### (4) peek()

- 스택에 가장 마지막에 추가한 원소를 반환한다.

```javascript
this.peek = function(){
  return items[item.length-1];
}
```

<br/>

### (5) isEmpty()

- 스택이 비어있으면 true, 스택에 하나라도 있으면 false를 반환한다.
```javascript
this.isEmpty = function(){
  return items.length == 0;
}

<br/>

### (6) size()

- 스택과 같으 컬랙션에서는 length 대신 size()라는 용어를 쓴다.

```javascript
this.size = function(){
  return items.length;
}
```

<br/>

### (7) clear()

- 스택의 모든 원소를 삭제하는 역할을 한다.
```javascript
this.clear = function(){
  items = [];
}
```

## 3) stack 클래스, 한눈에 보기

```javascript
function stack(){

  var items = [];
  
  this.push = function(e){
    items.push(e);
  }
  this.pop = function(){
    returm items.pop();
  }
  this.peek = function(){
    return items[items.length-1];
  }
  this.isEmpty = function(){
    return items.length == 0;
  }
  this.size = function(){
    return items.length;
  }
  this.clear = function(){
    items = [];
  }
  this.print = function(){
    console.log(items.toString());
  }

}

```

<br/>

## 4) stack 문제 풀어보기

### (1) 10828번, 스택

> 정수를 저장하는 스택을 구현한 다음, 입력으로 주어지는 명령을 처리하는 프로그램을 작성하시오. <br/> 명령은 총 다섯 가지이다. <br/><br/> push X: 정수 X를 스택에 넣는 연산이다. <br/> pop: 스택에서 가장 위에 있는 정수를 빼고, 그 수를 출력한다. 만약 스택에 들어있는 정수가 없는 경우에는 -1을 출력한다. <br/> size: 스택에 들어있는 정수의 개수를 출력한다. <br/> empty: 스택이 비어있으면 1, 아니면 0을 출력한다. <br/> top: 스택의 가장 위에 있는 정수를 출력한다. 만약 스택에 들어있는 정수가 없는 경우에는 -1을 출력한다. <br/><br/> 입력 <br/> 첫째 줄에 주어지는 명령의 수 N (1 ≤ N ≤ 10,000)이 주어진다. 둘째 줄부터 N개의 줄에는 명령이 하나씩 주어진다. 주어지는 정수는 1보다 크거나 같고, 100,000보다 작거나 같다. 문제에 나와있지 않은 명령이 주어지는 경우는 없다. <br/> <br/> 출력 <br/> 출력해야하는 명령이 주어질 때마다, 한 줄에 하나씩 출력한다.





## 2) 최댓값 문제

### (1) 설명

- 입력 : 9개의 수 입력

- 출력 : 최댓값이 몇번째에 입력됐는지 리턴

<br/>

### (2) 유용한 메소드

#### indexOf()

: 요소가 배열에서 몇번째에 위치했는지 출력해준다.

<br/>

#### Math.max.apply()

```jsx
var myArray = [-3, -2, 1, 3, 5];
var max = Math.max.apply(null, myArray);

5 // 최대값 5가 출력됨
```

<br/>

### (3) 코드 및 결과

```jsx
//1. 9번 반복하여 수 입력을 받고, 이 수를 배열에 저장한다.
var array = []
var count = 9

while(count > 0){
	var input_num = prompt('수를 입력하시오')    //배열들은 string 형태
	array.push(input_num);
	count --;
}

var max_num = Math.max.apply(null, array);  //number 형태

console.log(array.indexOf(String(max_num)))+1)  //형이 다르면 index가 안나옴

//2. 배열에서 제일 큰 값을 찾고, 그 값의 인덱스 값+1을 리턴한다.
```

<img src="https://postfiles.pstatic.net/MjAyMDA2MjVfMzUg/MDAxNTkzMDY1Mzk4MjQ2.bbp0nl_9pCW0Pthn4qlnDCeDY_mw0Q0-jQyu7qWft_sg.N6tEJCGp_Sgs3DV_QFVVUaZcki0c1RZkGjgRgJEPupcg.PNG.rmawjdals/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2020-06-25_%EC%98%A4%ED%9B%84_2.03.51.png?type=w580" style="width:50%"/>


<br/>

<br/>


## 3) 숫자의 개수 문제

### (1) 설명

- 입력 : 세 개의 자연수 입력

- 출력 : 세 개의 자연수를 곱한 결과값에서 0~9 숫자들의 개수를 출력

<br/>

### (2) 유용한 메소드

#### forEach()

```jsx
const array1 = ['a', 'b', 'c'];

array1.forEach(element => console.log(element));

// expected output: "a"
// expected output: "b"
// expected output: "c"

```


<br/>

### (3) 코드 및 결과

```jsx
var count = 3;        // 입력할 수의 개수
var array1 = [];      // 입력된 값들을 저장하는 배열
while(count > 0){
	var input_num = prompt('숫자를 입력하시오')
	array1.push(Number(input_num));        //계산을 위해 Number로 형변환
	count --;
}
var results = array1[0] * array1[1] * array1[2] //세 개의 곱 계산
var array2 = String(results).split('')          //split를 위해 String변환

var array3 = [0,0,0,0,0,0,0,0,0,0];               //숫자별 개수 저장 배열

//array2의 요소를 꺼내, 2가 나오면 -> array3의 2번째 배열 원소 값을 +1 증가시킴
array2.forEach((ele)=>{array3[Number(ele)] = array3[Number(ele)] + 1})
```

<img src="https://postfiles.pstatic.net/MjAyMDA2MjVfMzAg/MDAxNTkzMDY1Mzk4MjQw.rMCY_tGsAV5gfb4xvoQ_GgqPQI__THGDElSRX-chlCgg.pqL6W4FkDCoz0ovlDNnogHOao7QjiB34vlGI3j88b0Qg.PNG.rmawjdals/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2020-06-25_%EC%98%A4%ED%9B%84_2.24.10.png?type=w580" style="width:50%"/>





























