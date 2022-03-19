# 익명 함수

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

대부분의 함수는 갖지만 **익명 함수(Anonymous function)**라 불리는 이름 없는 함수를 만들 수도 있습니다. 익명 함수는 때때로 **람다(Lambda)** 또는 **클로저(Closure)**로 불립니다. 익명 함수도 함수이기 때문에 함수의 특징을 갖습니다. 익명 함수는 함수 이름을 생략하며 <mark style="color:green;">`()`</mark> 안에 함수 인자를 선언하고 <mark style="color:green;">`{}`</mark> 안에 함수 본문을 구현합니다.

<mark style="color:green;">`([[`</mark>_<mark style="color:green;">`Type`</mark>_<mark style="color:green;">`]`</mark><mark style="color:green;">` `</mark>_<mark style="color:green;">`param1`</mark>_<mark style="color:green;">`[, …]]) {`</mark>\
&#x20; <mark style="color:green;">``</mark><mark style="color:green;">`  `</mark>_<mark style="color:green;">`codeBlock`</mark>_<mark style="color:green;">`;`</mark>\ <mark style="color:green;">`};`</mark>

다음 예제는 타입이 선언되지 않은 <mark style="color:green;">`item`</mark>이라는 인자를 받는 익명 함수를 정의합니다. <mark style="color:green;">`list`</mark>의 각 항목에 대해서 호출된 함수는 인덱스와 값을 출력합니다.

```dart
void main() {
  const list = ['apples', 'bananas', 'oranges'];
  list.forEach((item) {
    print('${list.indexOf(item)}: $item');
  });
}
```

{% embed url="https://dartpad.dev/?id=79d6981bcbaee0f5596e5843d87545ef" %}

위와 같이 함수에 하나의 표현식만 존재할 경우 화살표 표현식을 사용하여 간단히 표현할 수 있습니다.

```dart
list.forEach((item) => print('${list.indexOf(item)}: $item'));
```
