# 4.  연결리스트

## 1) 연결리스트?

*사진 클릭시 사진 출처로 이동합니다.*

<a href="https://freestrokes.tistory.com/84"><img src="https://t1.daumcdn.net/cfile/tistory/99CEE2425CB7F7CB10"/></a>
 

: 동적인 자료구조로 필요할 때마다 원소를 추가, 삭제할 수 있다.

: 크기가 계속 변한다.

: 각 원소들은 원소 자신과 다음 원소를 가리키는 참조정보가 포함된 노드로 구성된다.

: 원소를 삭제하라면, 연결된 부분을 잠시 끊어야한다.(마치 기차 객차)

<br/>

## 2) 연결 리스트 만들기

: 연결 리스트를 나타내는 클래스를 직접 작성할 수 있다.

### (1) 연결 리스트 구현시 필수 메소드

- append(원소) : 리스트의 맨 끝에 원소를 추가한다.

- insert(위치, 원소) : 해당 위치에 원소를 삽입한다.

- remove(원소) : 원소를 삭제한다.

- indexOf(원소) : 해당 원소의 인덱스를 반환한다. 존재하지 않는 경우 -1을 반환한다.

- removeAt(위치) : 해당 위치에 있는 원소를 삭제한다.

- isEmpty() : 원소가 하나도 없다면 true, 그 외엔 false를 반환한다.

- size() : 원소 개수를 반환한다. 배열의 length()와 비슷한다.

- toString() : 연결리스트는 원소를 노드에 담기 때문에, 원소의 값만을 출력하려면 toString을 재정의해야한다.


<br/>

### (2) append()

- 연결리스트 끝에 원소를 추가할 때 빈 연결 리스트인지 여부에 따라 2가지 경우를 고려해야한다.

- 리스트가 비어있다면?
<img width="75%" src="https://blogfiles.pstatic.net/MjAyMDA5MDRfMTk4/MDAxNTk5MTk1MjI5MDUw.mXUgOR5b_bglAadGHIMQtZGqx0rBagaX3-8Va5q9190g.xdv44KBa48c0lQu1qkl-B7LNCf8BLkYCrNqQLOuQ0a0g.PNG.rmawjdals/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2020-09-04_%EC%98%A4%ED%9B%84_1.52.54.png"/>

: 연결리스트를 처음 생성하므로 head값은 null이다.

: 리스트에 해당 원소를 첫원소로 추가하고, head가 node를 가리키게 한다.

: 그러면 node.next가 자동으로 null이 된다.(연결리스트의 마지막노드의 next는 항상 null)

<br/>

- 리스트에 원소가 들어있다면?
<img width="75%" src="https://blogfiles.pstatic.net/MjAyMDA5MDRfMjk3/MDAxNTk5MTk1ODkzNjY0.bvNqa_0tdVzmmfpSM1r-ekc7UmgcKn1_AHAAymbx3ekg.zFYBXUeBTJr85J0EV5UeWADtYpNeGD8OAe9P2iwuTj8g.PNG.rmawjdals/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2020-09-04_%EC%98%A4%ED%9B%84_2.04.35.png"/>
: 리스트의 마지막 원소를 찾는다.

: 마지막 원소를 찾을 때까지 루프를 반복한다.(node.next가 null이면 마지막 원소임)

: 리스트의 현재 원소를 current에 담고, current.next가  null이 되는 시점에서 루프를 종료한다.

: 그러면 current가 바로 마지막 원소이므로, currnet.next에 추가할 원소를 가르키면 된다.


```javascript
this.append = function(element){
  
  var node = new Node(element);   //element로 node 생성
  var current;                    //현재원소를 담음 
  
  if(head == null){
    head = node;                  //head가 없으면 head에 노드를 넣음
  }else{                          //원소가 있다면
    current = head;   
    while(current.next){          //next가 null인 마지막 원소 찾기
      current = current.next;     // 다음을 탐색
    }
    current.next = node;          //next가 null인 current를 찾음
                                  //current의 next가 node를 가리키게 함 
  }
  length++;                       //길이 +1
};
```

<br/>


### (2) removeAt()

- 원소의 위치를 기준으로 삭제하는 메소드이다.

- 첫 번째 원소를 삭제하는 경우

<img width="75%" src="https://blogfiles.pstatic.net/MjAyMDA5MDRfMTM4/MDAxNTk5MTk3MjYxOTQw.8izTeg7aBgjVduHsVFDtXKR1vLBZEQVoDIPLLWgd8Sog.4jq3xs300wpjQig2WFOcZjmftzEsdXZ56CFul2EdLG0g.PNG.rmawjdals/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2020-09-04_%EC%98%A4%ED%9B%84_2.27.18.png"/>

:  head가 그 다음 원소를 가리키도록 바꿔야 한다.

: 현재 current는 head이다.
 
: head를 current.next로 바꾸면 첫 번째 원소가 삭제된다.

<br/>

- 마지막 혹은 중간의 원소를 삭제하는 경우

<img width="75%" src="https://blogfiles.pstatic.net/MjAyMDA5MDRfMTQg/MDAxNTk5MTk3MjYxOTUz.Vs_TJSY9VdnF4mpxKZWzrS2iZ95a3p1ENOt6IJB1Uesg.BwPJytrru1DHCLGBaXTferV6mMklo1_6jYpgzhb6-CAg.PNG.rmawjdals/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2020-09-04_%EC%98%A4%ED%9B%84_2.27.21.png"/>

: current변수는 삭제할 원소, previous는 삭제할 원소의 이전 원소이다.

: current원소를 삭제하려면 previous.next와 current.enxt을 똑같이 맞추면 된다.

```javascript
this.removeAt = function(position){

  //범위 외의 값인 체크한다.
  if(position > -1 && position < length){
    var current = head;
    var previous;
    var index = 0;
    
     //첫 번째 원소를 삭제하는 경우
     //current는 현재 head
    if(position == 0){
    head = current.next;  
    }
    
    //중간, 혹은 끝의 원소를 삭제하는 경우
    else{
      //삭제하려는 position번째 원소를 찾기
      while(index++ < position){
        previous = current;
        current = current.next;
      }
      
      //삭제하려는 current를 찾았다면?
      //현재의 다음과 이전 것을 연결한다.(삭제를 위해 건너띄는 것)
      previous.next = current.next; 
    }
    length--;
    return currnet.element;
  
  }else{
    return null;
  }
};

```

<br/>

### (3) insert()

- 임의의 위치에 원소를 삽입하는 메소드이다.

<img width="75%" src="https://blogfiles.pstatic.net/MjAyMDA5MDRfMTk3/MDAxNTk5MTk3Nzk4NDUz.wCAyl__NBcXIzHGME9CWEEifOerhXoM0VqtLotk8wP4g.UOQJSXyKntW5DUS64T_Kfz0OM9NUUVdYX11pKhGvGtgg.PNG.rmawjdals/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7_2020-09-04_%EC%98%A4%ED%9B%84_2.36.18.png"/>


```javascript
this.insert = function(position, element){
  //범위 외의 값인지 체크한다.
  if(position >=0 && position <= length){
    var node = new Node(element);
    var current = head;             //처음 시작위치
    var previous;
    var index = 0;                  //처음 시작인덱스
    
    //첫 번째로 추가
    if(position == 0){
      node.next = current;        //node.next는 원래 head
      head = node;                //node가 head가 됨
    }
    else{
      //넣으려는 위치를 찾는다.
      while(index++ < position){
        previous = current;     
        current = current.next;
      }
      //node를 previous, current사이에 삽입한다.
      node.next = current;       //(1)
      previous.next = node;      //(2)
    }
    length++;
    return true;
  }else{
    return false;
  }
};
```



<br/>

### (4) 그 밖의 메소드

- toString, indexOf, isEmpty, size에 대해 알아보자.

- toString() : 객체를 문자열로 변환한다. 

```javascript
this.toString = function(){
  //리스트의 모든 원소를 순회하기 위해 head를 시작점으로..
  //current변수를 인덱스 삼아 루프문을 실행
  var current = head;      
  string = '';
  
  while(current){
    string += current.element;
    current = current.next;
  }
  return string;
};
```

<br/>

- indexOf() : 원소값을 인자로 받아, 해당 원소의 인덱스르 반환한다.

```javascript
this.indexOf = function(element){
//리스트 순회를 위해 current를 시작점으로 함
  var current = head;
  var index = -1;
  
  while(current){
    //element와 현재위치의 element와 같다면? -> index 리턴
    if(element === current.element){
      return index;
    }
    //다르면 -> 계속 순회
    index++;
    current = current.next;
  }
  return -1;
};

```

<br/>

- indexOf() : 원소값을 인자로 받아, 해당 원소의 인덱스르 반환한다.

```javascript
this.indexOf = function(element){
//리스트 순회를 위해 current를 시작점으로 함
  var current = head;
  var index = -1;
  
  while(current){
    //element와 현재위치의 element와 같다면? -> index 리턴
    if(element === current.element){
      return index;
    }
    //다르면 -> 계속 순회
    index++;
    current = current.next;
  }
  return -1;
};

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



