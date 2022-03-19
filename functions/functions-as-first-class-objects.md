# 일급 객체로서의 함수

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:red;">Dart</mark>에서 함수는 **일급 객체(first-class objects)**입니다.

* 함수를 다른 함수에 매개변수로 전달할 수 있습니다.
* 함수 안에서 함수를 정의하고 함수의 반환값으로 함수를 사용할 수 있습니다.
* 변수에 함수를 할당할 수 있습니다.

```dart
void main(List<String> arguments) {
  var list = [1, 2, 3];
  
  // forEach 함수의 매개 변수로 printElement 함수를 전달합니다.
  list.forEach(printElement);

  // 익명 함수를 정의하여 loudify 변수에 할당합니다.
  var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
  
  // loudify 변수는 함수를 가르키므로 loudify 변수를 이용해 함수를 호출할 수 있습니다.
  print(loudify('hello'));
}

void printElement(int element) {
  print(element);
}
```

{% embed url="https://dartpad.dev/?id=41cc6a7ec0ce01ea57a1b7129a7b1cc1" %}
