# 2W_algorism

#문제

```
function solution(arr) {
    arr.splice(arr.indexOf(Math.min(...arr)),1);
    if(arr.length<1)return[-1];
    return arr;
}
```
----------------------------------------------------------------------------------------

* splice() : 원하는 위치에 요소를 추가하거나 삭제할수 있음
추가하고싶을때 : splice (추가를 원하는 인덱스, 0, 요소)
    const itemsA = [‘사과‘, ‘복숭아‘, ‘수박‘]
    itemsA.splice(1, 0, “체리“)
    itemsA => [‘사과‘, ‘체리‘, ‘복숭아‘, ‘수박‘]
삭제하고 싶을때 : splice (삭제를 원하는 인덱스, 제거할 요소의 개수)
ex)  const itemsA = [‘사과‘, ‘복숭아‘, ‘수박‘]
    itemsA.splice(2,1) => 배열의 2번째 인덱스로부터 1개의 요소를 제거
    itmesA => [‘사과‘, ‘복숭아‘]
* 값으로 요소 제거하기
const 인덱스 = 배열.indexOf(요소)
배열.splice(인덱스,1)
ex) const itemsA = [‘사과‘, ‘복숭아‘, ‘수박‘]
    const index = itemsA.indexOf(‘수박‘)
    index => 2 (배열 내부에 수박이 있으므로 해당 요소의 인덱스를 출력)
    itemsA.splice(2,1) => 2번째 인덱스에 있는 1개의 요소를 제거
    itemsA => [‘사과‘, ‘복숭아‘]
    itemsA.indexOf(‘수박’)
    * 수박은 배열에 없으므로 -1을 출력함
@ indexOf 메소드는 배열 내부에 요소가 있을 경우 인덱스를 리턴함.
 
 하지만 배열 내부에 요소가 없을 때는 -1을 리턴함
------------------------------------------------------------------------------------

Spread Operator (스프레드 연산자) -> ex (...arr)
// 기존 방식
```
var arr1 = [1,2,3];
var arr2 = [4,5,6];
var arr = arr1.concat(arr2);
console.log(arr); // [ 1, 2, 3, 4, 5, 6 ]
```
// spread operator
```
var arr1 = [1,2,3];
var arr2 = [4,5,6];
var arr = [...arr1, ...arr2];
console.log(arr); // [ 1, 2, 3, 4, 5, 6 ]
```
