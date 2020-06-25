# 1. 배열

## 1) 배열이란?

: 배열은 동일한 데이터 타입의 값들을 연속적으로 저장한다.

: *하지만 자바스크립트의 경우 다른 타입의 데이터를 배열에 넣을 수 있다.*

<br/>

## 2) 배열의 필요성

: 많은 변수를 요하는 데이터를 적은 변수의 사용으로 다룰 수 있게 한다.

<br/>

## 3) 배열의 생성과 초기화

### (1) 배열의 생성

#### 방법(1)

: `new` 키워드를 배열 인스턴스를 생성한다.

: `new` 키워드에 인자를 주면 배열의 크기를 지정할 수 있다.

```javascript
var day1 = new Array();
var day2 = new Array(10);

```

<br/>

#### 방법(2)

: `[]대괄호`를 이용하여 생성할 수도 있다.

```javascript
var day3 = []
```

<br/>

### (2) 배열의 초기화

```javascript
var days = ['a', 'b', 'c'];
```

<br/>

### (3) 배열의 길이

```javascript
console.log(days.length);
```

<br/>

### (4) 인덱스 접근

: 대괄호 안에 숫자를 넣어 요소에 접근할 수 있다.

: 아래 피보나치 수열을 통해 알아보자.

<img src="https://postfiles.pstatic.net/MjAyMDA2MjVfMjQg/MDAxNTkzMDYzMjg0NjQ0.X-9YZudopuX-OoP-CM0Edz22ywobbQswtqtPXK_Sc-0g.dhFfN37XHRXVgm1hRc3BySk6Or3mpCNp51n7nnpyrhMg.PNG.rmawjdals/_2020-06-24__1.41.55.png?type=w580" style="width:300px; "/>

```javascript
var fibonacci = [];   //값들을 저장하는 배열
fibonacci[1] = 1;    //1번째 수는 1
fibonacci[2] = 2;    //2번째 수는 2

for(var i=3; i<20; i++){
  fibonacci[i] = fibonacci[i-1] + fibonacci[i-2];
}

for(var i=1; i<fibonacci.length; i++){   //배열 안에 저장된 모든 값들을 출력
  console.log(fibonacci[i]);  
}
```

<br/>
<br/>

## 4) 원소 추가와 삭제

<br/>

### (1) 원소 추가

#### 가장 마지막 인덱스에 새 원소 추가

: 배열의 제일 `마지막 인덱스`에 값을 추가하려면 인덱스값을 `길이의 값`으로 하면 된다.

```javascript
var num = [1,2,3];
num[num.length] = 4;
```

<br/>

#### push 메소드

: 배열의 마지막 위치에 새 원소를 추가한다.

: 추가하고자 하는 원소를 인자에 적어주면 된다.

```javascript
num.push(4);   //[1,2,3,4]
num.push(5,6); //[1,2,3,4,5,6]
```
*push, pop 메소드는 스택 자료구조를 모방한 메소드이다.*

<br/>

#### unshift 메소드

: 배열 제일 앞에 새로운 원소를 추가한다.

: 제일 앞에 원소를 추가하기 위해, 기존 원소들의 인덱스는 `i -> i+1` 이 된다.

```javascript
num.unshift(0);      //[0,1,2,3,4,5,6]
num.unshift(-2,-1);  //[-2,-1,0,1,2,3,4,5,6]
```

<br/>

### (2) 원소삭제

#### pop 메소드

: 배열의 제일 마지막의 원소를 삭제한다.

```javascript
num.pop();   //[-2,-1,0,1,2,3,4,5,6]
```

<br/>

#### 배열 제일 앞을 삭제하는 방법(1)

: `i번째` 인덱스 자리에 `i+1번째`인덱스 값을 넣는다.

: 하지만 이 방법은 실제로 배열의 크기는 변하지 않기에 제일 마지막 인덱스에 잉여 원소가 존재한다.

```javascript
for(var i=0; i<num.length; i++){
  num[i] = num[i+1];
}
```

<br/>

#### 배열 제일 앞을 삭제하는 방법(2), `shift()`

: 잉여 원소를 남기지 않고, 제일 앞의 배열을 삭제한다.

```javascript
num.shift();  //[-1,-0,1,2,3,4,5,6]
```

<br/>

### (3) 특정 위치의 원소 삭제 

: splice(`시작`,`삭제할 개수`,`추가할 원소값들`)

```javascript
num.splice(5,3);      //인덱스5을 시작으로 3개의 값을 삭제
num.splice(5,0,2,3,4) //인덱스5을 시작으로 2,3,4추가
```

<br/>
<br/>

## 5) 2차원과 다차원 배열

: 표와 같이 데이터를 분류해야할 때 사용하는 배열이다.

<img src="https://t1.daumcdn.net/cfile/blog/240F8D3D5270EB9613" style="width:40%;"/>

*출처 : http://blog.daum.net/coolprogramming/17*

```javascript
function printMatrix(matrix){
	for(var i=0; i<matrix.length; i++){         
		for(var j=0; j<matrix[i].length; j++){
			console.log(matrix[i][j]);         //2차원 배열의 값을 출력하기
		}
	}
}
```

<br/>
<br/>

## 6) 유용한 배열 메소드

### (1) 여러 배열 합치기

```jsx
var zero = 0;
var pos = [1,2];
var naga = [-2,-1];

var num = naga.concat(zero, pos);  //-2,-1,0,1,2
// 대상배열.concat(뒤에 붙일 배열들)
```

<br/>

### (2) 반복자 함수

: 만약 2의 배수일 때 `true`를 리턴하는 함수가 있다고 하자.

: 아래 코드는 2의 배수면 `true`, 아니면 `false`를 리턴한다.


```jsx
var test = function(x){
	console.log(x);
	return (x%2==0) ? true : false;
}
```

<br/>

#### every(), false 나올때까지..

: x가 1이면 2의 배수가 아니므로 false를 리턴하고 반복을 중지한다.

<br/>

#### some(), true 나올때까지..

: x가 2일때 2의 배수이므로, true를 리턴하고 반복을 중지한다.

<br/>

#### 다른 반복문, forEach()

: 기존의 for문보다 forEach문이 더 효율적이다.

```jsx
//배열.forEach(function(인덱스){출력})

num.forEach(function(x){    // forEach안에 함수를 넣는다.
  console.log((x%2==0));    // 2의배수면 true, 아니면 false
})
```

<br/>

<hr/>

<br/>


# 2. 배열&백준알고리즘

## 1) 최솟값, 최댓값 문제

### (1) 설명

- 입력 : 정수의 개수 N, N개의 정수를 공백으로 구분하여 입력

- 출력 : 정수 N개의 최솟값, 최댓값 출력

<br/>

### (2) 사용한 메소드

#### 사용자의 입력 받기, `prompt()`

: prompt함수가 호출되면 입력창이 팝업되고 사용자의 입력을 기다린다.

<br/>

#### 문자열 분할, `.split()`

: .split()은 문자열을 분할하는 메서드이다. →  배열로 리턴

<br/>

#### 타입변환은 Number()와 String().

<br/>

#### 요소 변경, `map()`

```jsx
const arr = [0,1,2,3];

let squaredArr = arr.map(function(element){
    return element * element;
});
// 혹은 arrow 함수 가능
squaredArr = arr.map(element => element * element);

console.log(squaredArr); // [ 0, 1, 4, 9 ]
```

<br/>

#### 요소 정렬, sort()

```jsx
var fruit = ['a', 'c', 'b'];

fruit.sort(); // a, b, c
```

```jsx
//숫자 정렬
var score = [4, 11, 2, 10, 3, 1]; 

//오류
score.sort(); // 1, 10, 11, 2, 3, 4 
              // ASCII 문자 순서로 정렬되어 숫자의 크기대로 나오지 않음

//정상
score.sort(function(a, b) { // 오름차순
    return a - b;
    // 1, 2, 3, 4, 10, 11
});

score.sort(function(a, b) { // 내림차순 -> 반영되어 저장됨
    return b - a;
    // 11, 10, 4, 3, 2, 1
});
```

<br/>

### (3) 코드 및 결과

```jsx
//1. 자바스크립트에서 수 입력을 받는 방법
var number = prompt('');   //입력할 숫자의 개수    

//2. 개수들을 받음.
var nums = prompt('');  //string형

//3. string으로 받은 숫자들을 띄어쓰기를 중심으로 나눠서, 배열에 넣기 
var array1 = nums.split(' ');

//4. 배열 안에 있는 string을 number로 변환 -> map사용
var array2 = array1.map(ele => Number(ele));

//5. 숫자로 변환한 배열을 순서대로 정렬
array2.sort(function(a,b){
	return a - b;
});

//6. 배열에서 정렬 -> 0번째, 마지막 인덱스 값을 리턴
if(number == array2.length){
	colsole.log(array2[0], array2[array2.length-1])
}
```

<img src="https://postfiles.pstatic.net/MjAyMDA2MjVfMTMx/MDAxNTkzMDY1Mzk4MjQ5.p1eYgnifN_vmxRA47HV6hqf5MXKw78BKKmjhrxC5kUkg.RzcHZxJTVwk9KBpeTYJAh8_IdSqT1GA9ywt4oSVIEEAg.PNG.rmawjdals/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2020-06-25_%EC%98%A4%ED%9B%84_1.41.26.png?type=w580" style="width:50%;"/>

<br/>
<br/>

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





























