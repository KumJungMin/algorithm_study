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

### (1) <a href="https://www.acmicpc.net/problem/18258">18258번, 큐2</a>

```javascript
//1. 받을 명령의 개수
var input = prompt('명령의 개수를 입력하시오');
var box = [];

// 2. 명령의 개수만큼 반복
while(input > 0){
    let action = prompt('원하는 동작을 입력하시오');
    // push가 포함된 명령의 경우, 숫자만 추출하여 -> 입력
    QueueMethod(action);
    input = input-1;
}

function QueueMethod(action){
    var splitBox = action.split(' ')
    switch(splitBox[0]){
        case 'push':
            return(box.push(splitBox[1]));

        case 'pop':
            let popresult = box.shift();
            alert(popresult == undefined ? -1 : popresult);
            break;
        
        case 'size':
            alert(box.length);
            break;

        case 'empty':
            alert(box.length == 0 ? 1 : 0)
            break;
        
        case 'front':
            alert( box[0] == undefined ? -1 : box[0]);
            break;
        
        case 'back':
            alert(box[box.length-1] == undefined ? -1 : box[box.length-1]);
            break;
    }
    
}
```

<br/>

### (2) <a href="https://www.acmicpc.net/problem/2164">2164, 카드2</a>

```javascript
//1. n개의 카드가 주어진다.
card = prompt('카드의 개수를 입력하시오')
card_num = parseInt(card)
box = []
// 2.카드를 정렬한다.
for(var i=1; i<=card_num; i++){
    box.push(i);
};
alert(box);

//3. 
while(true){

//1,2,3,4
//0번째 버림
//0번째 버리고 -> 끝에 추가

    box.shift();
    alert('box=' + box);
    let move = box.shift();
    alert('box=' +  box);
    box.push(move);
    alert('box=' +  box);
    
    if(box.length == 1){
        alert(box[0]);
        break;
    }
}
```

<br/>

### (3) <a href="https://www.acmicpc.net/problem/11866">11866, 요세푸스 문제 0</a>

```javascript
//1. 1,2,3,4,5,6,7
// k = 3인 경우 [2번반복, 1번]
// shift()->push()
// shift()->push()
// shift()

// 1. n,k를 입력받는다.
var input = prompt('n k를 입력하시오');
var inputBox = input.split(' ');
var n = parseInt(inputBox[0]), k = parseInt(inputBox[1]);

var box = [], result = [];
//2. n개의 원소로 이루어진 배열 생성
for(var i=1; i<=n; i++){
    box.push(i);
}

// 3. k-1번 shift&push반복 | 1번 shift
while(true){
    for(let j=0; j<k-1; j++){
        let moveNum = box.shift();
        box.push(moveNum);
    }
    let resultNum = box.shift();
    result.push(resultNum);

    if(box.length == 0){
        alert(result);
        break;
    }

```

<br/>



