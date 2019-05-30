# forEach와 await

[Lantern2019]

피어슨 상관 계수에 의한 추천리스트를 받아서 user와 image src를 this.list1 배열에 넣어주었다.

```js
list.forEach(async ele => {
  const tmp = await this.$api.readUser(ele.id);
  tmp.src = await this.$storage.getUrl(`image/user/${ele.id}`);
  this.list1.push(tmp);
});
```

## 문제 상황

forEach() 함수에 async function을 인자값으로 사용했다.
this.list1의 순서가 유지되지 않았다.

```js
for (let i = 0; i < list.length; i++) {
  const tmp = await this.$api.readUser(list[i].id);
  tmp.src = await this.$storage.getUrl(`image/user/${list[i].id}`);
  this.list1.push(tmp);
}
```

## 실수/착각

forEach()는 단순히 다음 함수를 실행한다. 동기화를 기대하면 안 됐다.

다음은 ECMA-262의 forEach 소스코드이다.

주석 7. 번을 보면 while문 안에서 단순히 callbakc을 호출한다. async function을 callback으로 넘겨도 await을 호출하지 않으니까 동기화는 당연히 불가능하다.

```js
// Production steps of ECMA-262, Edition 5, 15.4.4.18
// Reference: http://es5.github.io/#x15.4.4.18
if (!Array.prototype.forEach) {
  Array.prototype.forEach = function(callback /*, thisArg*/) {
    var T, k;

    if (this == null) {
      throw new TypeError('this is null or not defined');
    }

    // 1. Let O be the result of calling toObject() passing the
    // |this| value as the argument.
    var O = Object(this);

    // 2. Let lenValue be the result of calling the Get() internal
    // method of O with the argument "length".
    // 3. Let len be toUint32(lenValue).
    var len = O.length >>> 0;

    // 4. If isCallable(callback) is false, throw a TypeError exception.
    // See: http://es5.github.com/#x9.11
    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }

    // 5. If thisArg was supplied, let T be thisArg; else let
    // T be undefined.
    if (arguments.length > 1) {
      T = arguments[1];
    }

    // 6. Let k be 0.
    k = 0;

    // 7. Repeat while k < len.
    while (k < len) {
      var kValue;

      // a. Let Pk be ToString(k).
      //    This is implicit for LHS operands of the in operator.
      // b. Let kPresent be the result of calling the HasProperty
      //    internal method of O with argument Pk.
      //    This step can be combined with c.
      // c. If kPresent is true, then
      if (k in O) {
        // i. Let kValue be the result of calling the Get internal
        // method of O with argument Pk.
        kValue = O[k];

        // ii. Call the Call internal method of callback with T as
        // the this value and argument list containing kValue, k, and O.
        callback.call(T, kValue, k, O);
      }
      // d. Increase k by 1.
      k++;
    }
    // 8. return undefined.
  };
}
```

## 해결방안

forEach()대신 js native for를 사용했다.
