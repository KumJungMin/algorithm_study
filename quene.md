# 3.  큐

## 1) 큐?

: 선입선출(Fast In First Out)으로, 먼저 들어간 게 먼저 나오는 구조이다.

: 마치 줄서기와 같으면, 출력물 인쇄대기에서 큐를 사용한다.

: 스택과 다르게 큐는 dequeue(), front()가 있다.

<br/>

## 2) 큐 만들기

: 큐를 나타내는 클래스를 직접 작성할 수 있다.

### (1) 스택 구현시 필수 메소드

- enqueue(원소(들)) : 큐의 뒤쪽에 원소를 추가한다.

- dequene() : 큐의 첫번째 원소(맨 앞)를 반환하고 삭제한다.

- front() : 큐의 첫번째 원소를 반환한다.

- isEmpty() : 큐가 비어있으면 true, 아니면 false를 반환한다.

- size() : 큐의 원소 개수를 반환한다.(배열의 length()와 같음)


<br/>

### (2) enqueue()

- enqueue()는 큐에 원소를 추가하는 메소드로, 큐의 뒤쪽으로만 추가한다.

- 단, 스택의 top에마 원소를 넣을 수 있다.

```javascript
var items = [];

this.enqueue = function(element){
  items.push(element);
}
```

<br/>

### (3) dequeue()

- 큐에서 가장 처음에 추가한 원소를 삭제한다.

- shift()는 배열에서 인덱스 0인 원소를 삭제한다.

```javascript
this.dequeue= function(){
  return items.shift();
}
```

<br/>

### (4) front()

- 큐의 맨 앞에 있느 원소가 무엇인지 알아낸다.

```javascript
this.front = function(){
  return item[0];
}
```

<br/>

### (5) isEmpty()

- 큐가 비어있으면 true, 스택에 하나라도 있으면 false를 반환한다.
```javascript
this.isEmpty = function(){
  return items.length == 0;
}

<br/>

### (6) size()

- 스택의 size()와 같다.

```javascript
this.size = function(){
  return items.length;
}
```


## 3) stack 클래스, 한눈에 보기

<a href="https://velog.io/@pa324/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-Queue%ED%81%90-udjxr0hb3x"><img width="40%;" src="https://media.vlpt.us/post-images/pa324/392c0570-9fa4-11e9-b079-63bbcd31f7a4/image.png" /></a>


```javascript
function Queue(){
  var items = [];
  
  this.enqueue = function(element){
    items.push(element);
  }
  this.dequeue = function(){
    return items[0];
  }
  this.isEmpty = function(){
    return items.length == 0;
  }
  this.clear = function(){
    items = [];
  }
  this.size = function(){
    return items.length;
  }
  this.print = function(){
    console.log(items.toString());
  }
}

```

## 4) 여러가지 큐 

### (1) 우선순위대로 들어가는 우선순위큐

- 일반적인 큐와 달리, 우선순위에 따라 원소가 추가되고 삭제된다.

- 우선순위큐는 우선순위 대로 들어가거나, 우선순위대로 삭제되는 2가지 경우가 있다.

- 실생활에서 1등석과 비즈니스석 승객은 항상 코치석 승객보다 우선순위가 늪은 것과 같다.


```javascript
function PriorityQueue(){
  var items = [];
  
  function QueueElement (element, priority){      //(a)
    this.element = element;
    this.priority = priority;
  }
```
(a) : 큐 원소에 우선순위가 부가된 새로운 형태의 원소이다.

```javascript
  this.enqueue = function(element, priority){
    var queueElement = new QueueElement(element, priority);
    
    if(this.isEmpty()){
      items.push(queueElement);                  //(b)
    }
```
(b) : 큐가 비어있으면 그냥 원소를 넣는다.

```javascript
    else{
      var added = false;
      for(var i=0; i<items.length; i++){
        if(queueElement.priority < items[i].priority){
          items.splice(i, 0, queueElement);     //(c)
          added = true;
          break;                                //(d)
        }
      }
      if(!added){                               //(e)
        items.push(queueElement);
      }
    }
  };
  
  //기본 큐와 동일한 메소드
}

```

(c) 새원소와 기존원소 비교

: 큐가 비어있지 않으면 먼저 기존 원소들과 우선순위를 비교한다.

: 만약 새 원소보다 기존원소의 우선순위가 더 높다면, 한칸 앞에 새 원소를 추가해준다.

: 이때 Array.slice(인덱스, 삭제할 개수, 넣을 원소)를 사용하여 추가한다.

<br/>

(d) : 루프가 종료된다.

(e) : 만약, 새 원소의 우선순위가 가장 낮다면 큐의 맨 뒤에 추가한다.



<br/>

### (2) 환형 큐

- 환형큐는 뜨거운 감자 게임과 같다.

```
뜨거운 감자게임이란, 원형 테이블에 앉아있는 아이들이 뜨거운 감자를 옆 사람에게 넘긴다.
그러다가 갑자기 모두 동작을 멈추구 그때 뜨거운 감자를 손에 들고 있는 아이가 벌칙으로 퇴장하는 방식이다.
이 게임은 최후의 1인이 남을 때까지 반복한다.
```


<br/>

## 5) stack 문제 풀어보기

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





