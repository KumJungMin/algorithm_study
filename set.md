# 5. 집합

## 1) 집합이란?

: 정렬되지 않은 컬렉션이다.

: 중복된 원소를 포함하지 않는다.

: 집합은 합집밥, 교집합, 차집합 같은 수학적 연산도 가능하다.

<br/>

## 2) 집합 만들기

- set클래스의 기본 뼈대는 아래와 같다.

```javascript
function Set(){
  var items = {};
}
```

### (1) 집합 구현시 필수 메소드

- add(원소) : 원소를 추가한다.

- remove(원소) : 원소를 삭제한다.

- has(원소) : 어떤 원소가 집합에 포함되어 있는지 여부를 true, false로 반환한다. 

- clear() : 모든 원소를 삭제한다.

- size() : 원소 개수를 반환한다. 배열의 length와 비슷하다.

- values() : 집합의 모든 원소를 배열형태로 반환한다.



<br/>

### (2) has(원소)

- 집합의 모든 원소는 객체에 담겨 있으므로 in 연산자로 해당 원소가 items에 있는지 확인한다.

```javascript
//방법1
this.has = function(value){
  return value in items;
}

//방법2
this.has = function(value){
  retrun items.hasOwnProperty(value);
}
```

<br/>

### (3) add()

- 집합에 새 원소를 추가하는 메소드이다.

```javascript
this.add = function(value){
  if(!this.has(value)){
    items[value] = value;    //키,값 동일하게 저장
    return true;
  }
  return false;
}
```

<br/>

### (4) remove, clear()

- remove()는 삭제할 원소가 집합에 존재하는지 확인하고, 해당 원소가 있다면 삭제한다.

```javascript
this.remove = function(value){
  if(this.has(value)){
    delete items[value];   //delete연산자 사용
    return true;
  }
  return false;
}
```

- 집합의 모든 원소를 삭제하고 싶다면 clear()를 사용한다.
```javascript
this.clear = function(){
  items {};
}
```


<br/>

### (5) size()

- Object에는 key라는 메소드가 있는데, 객체의 모든 property를 배열로 반환한다.

- 따라서, 이 배열의 length로 원소개수를 파악할 수 있다.

```javascript
this.size = function()}{
  return Object.keys(items).length;
}
```

<br/>

### (6) values()

- Object에는 key라는 메소드를 사용해 value값을 반환한다.

```javascript
this.values = function(){
  return Object.keys(items);
}
```

<br/>

## 2) 집합 연산

### (1) union(), 합집합

*이미지 클릭시 이미지 출처로 이동합니다.*

<a href="https://mathbang.net/10"><img src="https://t1.daumcdn.net/cfile/tistory/11434233502E0B4C2F"/></a>

- 합집합은 두 집합 중 어느 한 쪽이라도 포함된 원소로 구성된 집합이다.

```javascript
this.union = function(otherSet){
  var unionSet = new Set();       //합집합 생성
  
  var values = this.values();     //첫번째집합의 모든 value를 추출
  for(var i=0; i<values.length; i++){  //합집합에 value를 추가
    unionSet.add(values[i]);
  }
  
  values = otherSet.value();      //두번째집합의 모든 value를 추출
  for(var i=0; i<values.length; i++){  //합집합에 value를 추가
    unionSet.add(values[i]);
  }
  return unionSet;
};
```

<br/>


### (2) intersection(), 교집합

*이미지 클릭시 이미지 출처로 이동합니다.*

<a href="https://mathbang.net/10"><img src="https://t1.daumcdn.net/cfile/tistory/145A8333502E0B4C0A"/></a>

- 교집합은 두 집합 모두 포함되어 있는 원소로 구성된 집합이다.

```javascript
this.intersection = function(otherSet){
  var intersectionSet = new Set();    //교집합 생성
  
  var values = this.value();          //첫번째 집합의 모든 value추출
  for(var i=0; i<values.length; i++){
    if(otherSet.has(values[i])){       //다른집합에 같은 값이 있다면?
      intersectionSet.add(values[i]);  //교집합에 해당 값 추가
    }
  }
  return intersectionSet;
}
```

<br/>

### (3) difference(), 차집합

*이미지 클릭시 이미지 출처로 이동합니다.*

<a href="https://mathbang.net/11"><img src="https://t1.daumcdn.net/cfile/tistory/15130245502E083F28"/></a>

- 차집합은 첫번째 집합에는 있지만 두번째 집합에는 없는 원소로 구성된 집합이다.

```javascript
this.difference = function(otherSet){
  var differentSet = new Set();     //차집합 생성
  
  var values = this.values();       //첫번째 집합의 값 추출
  for(var i=0; i<values.length; i++){
    if(!otherSet.has(values[i])){   //두번째 집합에 해당 값이 없다면
      differentSet.add(values[i]);  //차집합에 추가
    }
  }
  return differenceSet;
}
```

<br/>

### (3) subset(), 부분집합

*이미지 클릭시 이미지 출처로 이동합니다.*

<a href="https://ko.wikipedia.org/wiki/%EB%B6%80%EB%B6%84%EC%A7%91%ED%95%A9"><img src="https://upload.wikimedia.org/wikipedia/commons/a/a8/Set_subsetAofB.svg"/></a>

- 부분집합은 어떤집합이 다른 집합의 일부인지 확인한다.

```javascript
this.subset = function(otherSet){
  //두 집합의 크기를 비교
  //만약 this가 otherSet보다 원소가 맞다면, 이미 부분집합 조건이 아님
  if(this.size() > otherSet.size()){
    return false;
  }
  else{
    var values = this.values();         //this의 values 추출
    for(var i=0; i<values.length; i++){
      if(!otherSet.has(values[i])){     //otherSet이 this의 값이 없다면 false
        return false;
      }
    }
    return true;
  }
}
```
