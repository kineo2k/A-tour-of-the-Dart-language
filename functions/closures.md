# 클로저

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

**클로저(Closure)**는  함수가 원래 범위 외부에서 사용되는 경우에도 어휘 범위의 **변수(Free variable)**에 접근할 수 있도록 하는 객체입니다. 함수는 주변 범위의 변수를 캡처할 수 있습니다. 다음 예제에서 <mark style="color:green;">`makeAdder()`</mark>는 변수 <mark style="color:green;">`addBy`</mark>를 캡처하여 클로저를 생성합니다.&#x20;

```dart
void main() {
  // 매개변수로 받은 정수값에 2를 더하는 클로저를 생성합니다.
  var add2 = makeAdder(2);

  // 매개변수로 받은 정수값에 4를 더하는 클로저를 생성합니다.
  var add4 = makeAdder(4);

  // 클로저를 어디에서 어떻게 사용해도 클로저가 캡처한 변수는 기억됩니다.
  print(add2(3));
  print(add4(3));
  printSum(add2, 10);
  printSum(add4, 10);
}

Function makeAdder(int addBy) {
  return (int i) => addBy + i;
}

void printSum(Function adder, int delta) {
  print(adder(delta));
}
```

{% embed url="https://dartpad.dev/?id=654435bd72357c0af607c596afe9a5ee" %}
