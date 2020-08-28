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

### (1) <a href="https://www.acmicpc.net/problem/10828">10828번, 스택</a>

```javascript
// 명령입력받기
var input = prompt('명령의 수를 입력하시오');
// 스택 저장소
var box = []

// 명령수만큼 반복
while(input > 0){
    // 명령입력받기
    var text = prompt('명령하시오');
    stackFunc(text);
    input = input-1;
}


// 함수
// push X일시 box에 X가 추가 
function stackFunc(text){
    // 받은 text에 push라는 말이 있다면?
    // 띄어쓰기 단위로 잘라서 -> 마지막 인덱스만 쟁취(형변환)
    if(text.includes('push')){
        splitText = text.split(' ');
        box.push(parseInt(splitText[1])) 
    }
    else if(text.includes('pop')){
        let pops = box.pop();
        pops === undefined ? alert(-1) : alert(pops)
    }
    // size: 스택에 들어있는 정수의 개수를 출력한다.
    else if(text.includes('size')){
        alert(box.length);
    }
    //empty: 스택이 비어있으면 1, 아니면 0을 출력한다.
    else if(text.includes('empty')){
        box.length === 0 ? alert(1) : alert(0)
    }
    //top: 스택의 가장 위에 있는 정수를 출력한다. 만약 스택에 들어있는 정수가 없는 경우에는 -1을 출력한다.
    else if(text.includes('top')){
        box.length === 0 ? alert(-1) : alert(box[box.length-1])
    }

}
```

<br/>

### (2) <a href="https://www.acmicpc.net/problem/10773">10773, 제로</a>

```javascript
// 정수가 "0" 일 경우에는 가장 최근에 쓴 수를 지우고, 아닐 경우 해당 수를 쓴다.
// 재민이가 최종적으로 적어 낸 수의 합을 출력한다. 
// 1. 입력할 숫자의 개수를 받음
var input = prompt('재민아, 입력할 숫자의 개수를 말해죠!')
var box = []
var sum = 0
while(input > 0){
    // 2. 수를 입력받는다.
    var nums = parseInt(prompt('수를 말해주세요'))

    // 3. 만약 입력받은 수가 0이면 -> pop() | 아니면 stack에 넣음
    nums == 0 ? box.pop() : box.push(nums)

    input = input - 1;
}

for(var value of box){
    sum = sum + parseInt(value) 
}
alert(sum);

// 4. 마지막에 stack의 합을 출력
```

<br/>

### (3) <a href="https://www.acmicpc.net/problem/9012">9012, 괄호</a>

```javascript
// 4. 스택배열(box)에 arr원소를 하나씩 push
function vps(arr){
    let box = []                        
    for(let value of arr){
        // 4-1. box가 비어있거나, box의 끝값이 ")"이고 push값이 "(" 그냥 push
        if(box.length == 0 || value == "(" && box[box.length-1] == ")"){
            box.push(value);            
            alert("box:" + box, "push:" + value)        //괄호흐름확인
        }

        // 4-2. box안에 있는 문자가 "("이고 push값이 ")"이면 -> (,)이므로 box를 pop
        else if(value == ")" && box[box.length-1] == "("){
            box.pop();                  
            alert("box:" + box, "push:" + value)
        }
        //4-3. 그 이외는 push
        else{
            box.push(value);          
            alert("box:" + box, "push:" + value)
        } 
    }
    (box.length == 0) ? result.push('YES') : result.push('NO')
}


var input = prompt('입력할 개수')              //1. 입력할 개수
var result = [];

while(input > 0){
    sample = prompt('괄호조합을 입력받음');      //2. 괄호조합을 입력
    let arr = sample.split('');            // 3. 괄호조합을 배열로 변경

    vps(arr);
    input = input - 1;
}
alert(result)                        


```

<br/>


### (4) <a href="https://www.acmicpc.net/problem/4949">4949, 균형잡인 세상</a>

#### 정규식으로 특정 문자, 숫자 등 제외하기
- 정규식 표현

```js
function onlyNumber(str) {

    var pattern_special = /[~!@\#$%<>^&*\()\-=+_\’]/gi,
        pattern_kor = /[ㄱ-ㅎ가-힣]/g,
        pattern_eng = /[A-za-z]/g;

    if (pattern_special.test(str) || pattern_kor.test(str) || pattern_eng.test(str)) {
        return str.replace(/[^0-9]/g, "");
    } else {
        return false;
    }

}
```

[옵션] : g(전체 검사), i(대소문자 모두 검사)

[숫자만추출] : /[a-z]/gi

[문자만추출] : /[1-9]/gi

[공백제거] : str1.replace(/(\s*)/g, "")


<br/>

- string.replace( 'string1', 'string2' )

: string에서 string1을 찾아 string2로 바꾼다.


<br/>

```javascript
var result = []
function onlySpecial(str) {  
    let pattern_eng = /[A-za-z]/g

    if (pattern_eng.test(str)) {                        
        let test1 = str.replace(/[a-z]/gi, "");        
        let test2 = test1.replace(/(\s*)/g, "");      
        // /[a-z]/gi
        
        alert(test2.split(''))
        return test2.split('')
    } else {
        return false;
    }

}


// 3. (), []를 판단하는 함수 작성
function vps(arr){
    let box = []                        
    for(let value of arr){
        
        // 4-1. box가 비어있거나, box의 끝값이 ")"이고 push값이 "(" 그냥 push
        if(box.length == 0 || (value == "(" && box[box.length-1] == ")") || (value == "[" && box[box.length-1] == "]")){
            box.push(value);            
            alert("box:" + box, "push:" + value)        //괄호흐름확인
        }

        // 4-2. box안에 있는 문자가 "("이고 push값이 ")"이면 -> (,)이므로 box를 pop
        else if((value == ")" && box[box.length-1] == "(") || (value == "]" && box[box.length-1] == "[")){
            box.pop();                  
            alert("box:" + box, "push:" + value)
        }
        //4-3. 그 이외는 push
        else{
            box.push(value);          
            alert("box:" + box, "push:" + value)
        } 
    }
    (box.length == 1) ? result.push('YES') : result.push('NO')
}




// 1. 입력받는다.
// 2. 입력의 종료조건으로 맨 마지막에 점 하나(".")가 들어온다.
while(true){
    let input = prompt('문자를 입력하시오');
    if(input == '.'){
        break;
    }else{
        let specText = onlySpecial(input);          //오직, 괄호만 남은 배열
        try {
            vps(specText)
        } catch (TypeError) {                       //첫글자에 띄우고, 정규식 이후 배열에 괄호가 없는 경우 때 에러 " ."
            result.push('YES');    
        }
    }
}
alert(result)                     


```





