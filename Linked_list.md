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

<br/>


- isEmpty() : 리스트에 원소가 하나라도 있으면 true, 아니면 false를 반환한다.

- size() : 리스트의 크기를 반환한다.

```javascript
this.isEmpty = function(){
 return length === 0;
}

this.size = function(){
 return length;
}

this.getHead = function(){
 return head;
}
```

<br/>

## 3) 이중연결리스트란

- 이중연결리스트는 이전&다음노드, 총 2개의 연결정보를 가지고 있다.


*사진 클릭시 사진 출처로 이동합니다.*


<a href="https://untitledtblog.tistory.com/84"><img width="75%" src="https://t1.daumcdn.net/cfile/tistory/243D4C4B5765630C05"/></a>


- 아래 코드를 보면...

```javascript
function DoublyLinkedList(){
 var Node = function(element){
  this.element = element;
  this.next = null;
  this.prev = tull;       //추가
 };
 
 var length = 0;
 var head = null;
 var taul = null;         //추가
}

```

: 아래 코드를 보면 알 수 있듯이, LinkedList와는 달리 2가지가 추가된다.

: 이전의 연결리스트의 경우 순회시 원소를 찾지 못하면 다시 맨 처음으로 돌아가야한다.

: 하지만, 이중연결리스트의 경우 이전&이후노드가 다 연결되어 있으므로 재 순회할 필요가 없다.

<br/>

### (1) 임의의 위치에 원소 삽입

- 이중연결리스트는 next, prev, 링크가 2개가 있다.

: 원하는 위치에 도달할 때까지 루프를 반복하면 `current`, `previous`원소 사이에 `node를` 넣는다.

: previous는 position-1위치인 노드, current는 position위치의 노드이다.

: `[node.next 연결]` 먼저, node의 다음을 current로 둔다. 

: `[previous.next 재연결]` 두 번째, previous의 다음을 노드로 하여 연결을 유지한다.

: `[current.prev 재연결]` 세 번째, current의 이전이 node를 가리킨다.

: `[node.prev 연결]` 네 번째, node의 이전을 previous로 둔다.

```javascript
this.insert = function(position, element){
 //범위 외의 값인지 체크한다.
 if(position >=0 && position <=length){
  var node = new Node(element),
   currrent = head,
   previous,
   index = 0;
   
   //첫 번째 위치에 추가
   if(position == 0){
    if(!head){        //head가 없으면 -> node가 head, tail이 됨 
     head = node;
     tail = node;
    }
    else{
     node.next = current;  //head앞에 node추가
     current.prev = node;  //head이전값은 node
     head = node;          //head는 이제 node
    }
   }
   //마지막 위치에 추가 
   else if(position == length){
    current = tail;
    current.next = node;  //tail다음은 node
    node.prev = current;  //node이전은 tail
    tail = node;          //node가 이제 tail
   }
   //중간 위치에 추가
   else{
   //position-1, position위치의 노드를 찾음(pre, curr)
    while(index++ < position){
     previous = current;
     current = current.next;
    }
    node.next = current;     //node다음은 currnet(position위치 노드)
    previous.next = node;    //previous(position-1)다음은 노드
    node.prev = previous;    //node 이전은 previous(position-1)
   }
   length++;
   return true;
 }else{
  return false;
 }
};
```




<br/>

## 5) 연결리스트 문제 풀어보기

### (1) <a href="#">번, </a>

```javascript

```

<br/>

