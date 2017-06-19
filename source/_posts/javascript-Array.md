---
title: 자바스크립트 배열(Array)
date: 2017-06-20 00:19:31
tags: javascript
---

# 배열(Array)

### 1. 배열 만들기

리터럴 방식 ) var menus = ["menu1", "menu2", "menu3", "menu4"];

생성자 방식 ) var menus = new Array("menu1", "menu2", "menu3", "menu4");

------

### 2. 배열 요소의 개수

배열의 프로퍼티 중 length를 이용하여 배열 요소의 개수를 알아낼 수 있다.

```javascript
var users = ["user1", "user2", "user3", "user4"];
console.log(user.length); // 결과 : 4	
```

------

### 3. 특정 위치의 배열 요소에 접근하기

```javascript
var menus = ["menu1", "menu2", "menu3", "menu4"];
for( var i=0; i<menus.length; i++){
  var menu = menus[i];
  console.log(menu);
}	
```

------

### 4. 배열을 문자열로 만들기

```javascript
var menus = 배열.join([매개변수]);
```

매개변수 : 선택사항이며, 배열 요소를 구분하기 위해 사용한다. 생략하게 되면 쉼표가 구분자로 사용된다.

```javascript
var menus = ["menu1", "menu2", "menu3", "menu4"];
var result = menus.join("-");
console.log(result);
// 구분자를 "-"로 사용하여 문자를 만들어 줌 
// 결과 : "menu1-menu2-menu3-menu4"
```

------

### 5. 문자열을 배열로 만들기

```javascript
var menuData = "menu1,menu2,menu3,menu4";
var menus = menuData.split(",");
for( var i=0; i<menus.length; i++){
  var menu = menus[i];
  console.log(menu);
}
```

------

### 6. 특정 위치에 배열 요소 추가하기

#### 6-1. 배열의 마지막 위치에 추가

```javascript
var menus = ["menu1", "menu2", "menu3", "menu4"];
console.log("menus : "+ menus.join(","));
// menus : menu1,menu2,menu3,menu4

menus.push("menu5");
console.log("newMenus : "+menus.join(","));
// newMenus : menu1,menu2,menu3,menu4,menu5
```

#### 6-2. 배열의 첫 번째 위치에 추가

```javascript
var menus = ["menu1", "menu2", "menu3", "menu4"];
console.log("menus : "+ menus.join(","));
// menus : menu1,menu2,menu3,menu4

menus.unshift("menu5");
console.log("newMenus : "+menus.join(","));
// newMenus : menu5,menu1,menu2,menu3,menu4
```

#### 6-3. N번째 위치에 추가

사용법 ) var result = 배열.splice(시작위치, 삭제할 요소의 갯수(0을 적용하면 추가함), [추가할요소])

```javascript
var menus = ["menu1", "menu2", "menu3", "menu4"];
console.log("menus : "+ menus.join(","));
// menus : menu1,menu2,menu3,menu4

menus.splice(2,0,"menu5");
console.log("newMenu : "+menus.join(","));
// newMenus : menu1,menu2,menu5,menu3,menu4
```

------

### 7. 특정 위치의 배열 요소 삭제하기

#### 7-1. 첫 번째 요소 삭제하기

```javascript
var menus = ["menu1", "menu2", "menu3", "menu4"];
console.log("menus : "+ menus.join(","));
// menus : menu1,menu2,menu3,menu4

menus.shift();
console.log("newMenu : "+menus.join(","));
// newMenus : menu2,menu3,menu4
```

#### 7-2. 마지막 요소 삭제하기

```javascript
var menus = ["menu1", "menu2", "menu3", "menu4"];
console.log("menus : "+ menus.join(","));
// menus : menu1,menu2,menu3,menu4

menus.pop();
console.log("newMenu : "+menus.join(","));
// newMenus : menu1,menu2,menu3
```

#### 7-3. N번째 요소 삭제하기

```javascript
var menus = ["menu1", "menu2", "menu3", "menu4"];
console.log("menus : "+ menus.join(","));
// menus : menu1,menu2,menu3,menu4

menus.splice(2,1);
console.log("newMenu : "+menus.join(","));
// newMenus : menu1,menu2,menu4
```

------

### 8. 정렬하기

#### 8-1. sort() 메소드

배열 요소를 오름차순 또는 내림차순으로 정렬해준다.

사용법 ) var result = 배열.sort(compareFunction);

sort() 함수는 배열 요소를 모두 문자열로 간주하고 알파벳순으로 정렬하기 때문에 비교 함수가 필요하다.

compareFunction : 정렬 순서를 정의하는 함수로 생략할 경우 오름차순으로 처리한다. 

```javascript
var userNames = ["bbb", "ddd", "ccc", "aaa"];
console.log("userNames : "+userNames.join(","));
// userNames : bbb,ddd,ccc,aaa

userNames.sort();
console.log("newUserNames : "+userNames.join(","));
// newUserNames : aaa,bbb,ccc,ddd
```

#### 8-1-1. 내림차순 정렬(큰 것 -> 작은 것)

```javascript
var userNames = ["bbb", "ddd", "ccc", "aaa"];
console.log("userNames : "+userNames.join(","));
// userNames : bbb,ddd,ccc,aaa

userNames.sort(function(a,b){
  return b > a;
});
console.log("newUserNames : "+userNames.join(","));
// newUserNames : ddd,ccc,bbb,aaa
```

#### 8-2. 숫자 정렬

##### 8-2-1. 오름차순

```javascript
var aryData = [5,2,8,9,3,6,4,1,77];
console.log("aryData : "+ aryData.join(","));
// aryData : 5,2,8,9,3,6,4,1,77

aryData.sort(function(a,b){
  return a-b;
});
console.log("newAryData : " + aryData.join(","));
// newAryData : 1,2,3,4,5,6,8,9,77
```

##### 8-2-2. 내림차순

```javascript
var aryData = [5,2,8,9,3,6,4,1,77];
console.log("aryData : "+ aryData.join(","));
// aryData : 5,2,8,9,3,6,4,1,77

ary.Data.sort(function(a, b){
  return b-a;
});
console.log("newAryData :"+ aryData.join(","));
// newAryData : 77,9,8,6,5,4,3,2,1
```

------

##### * compareFunction

뺄셈의 결과가 음수라는 것(a - b)은 왼쪽 숫자가 오른쪽 숫자보다 작다는 것을 의미한다.(오름차순)

뺄셈의 결과가 양수라는 것(b - a)은 왼쪽 숫자가 오른쪽 숫자보다 크다는 것을 의미한다.(내림차순)

```javascript
var compareFunction1 = function(num1, num2) {
  return num1 - num2;
};

var compareFunction2 = function(num1, num2) {
  return num2 - num1;
};
```

------

#### 8-3. object 정렬

```javascript
var student = [
    { name : "정", age : 21},
    { name : "이", age : 25},
    { name : "박", age : 13},
    { name : "김", age : 44}
]

/* 이름순으로 정렬 */
student.sort(function(a, b) { // 오름차순
    return a.name < b.name ? -1 : a.name > b.name ? 1 : 0;
    // 김, 박, 이, 정
});

student.sort(function(a, b) { // 내림차순
    return a.name > b.name ? -1 : a.name < b.name ? 1 : 0;
    // 정, 이, 박, 김
});

/* 나이순으로 정렬 */
var sortingField = "age";

student.sort(function(a, b) { // 오름차순
    return a[sortingField] - b[sortingField];
    // 13, 21, 25, 44
});

student.sort(function(a, b) { // 내림차순
    return b[sortingField] - a[sortingField];
    // 44, 25, 21, 13
});
```

------

### 9. 그 외 메소드

#### 9-1. reverse()

배열 안에 있는 원소들의 순서를 반대로 정렬하여 반환한다.

```javascript
var ary = ["red", "blue", "yellow", "orange"];

console.log(ary.reverse());
// ["orange", "yellow", "blue", "red"]
```

#### 9-2. concat()

배열 뒤에 각 전달인자들을 이어붙여 배열을 새롭게 생성하여 반환한다.

```javascript
var ary = ["red", "blue", "yellow", "orange"];
var ary2 = ["green", "white"];

console.log(ary.concat(ary2));
// ["orange", "yellow", "blue", "red", "green", "white"] 
```

#### 9-3. toString()

배열의 원소를 문자열로 반환한다.

```javascript
var ary = ["red", "blue", "yellow", "orange"];

console.log(ary.toString());
// "red","blue","yellow","orange"
```

#### 9-4. indexOf()

배열 내부에서 찾고자 하는 값이 존재하는지를 알려준다.

존재하지 않는다면 "-1"을 반환하고, 존재한다면 가장 첫 번째의 인덱스를 반환한다. 

첫 번째 인자는 찾고자 하는 값이고 두 번째 인자는 찾고자 하는 범위이다.

```javascript
var a = [0, 1, 2, 3, 4];
a.indexOf(1); // 반환값은 1
a.indexOf(5); // 반환값은 -1
```

------

*이상으로 배열에 관한 간단한 설명과 자주 쓰이는 메소드들을 정리했다.*

*더 많은 메소드들은 MDN에서 찾으며 공부하자 !*

#### [LINK : Array MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array)