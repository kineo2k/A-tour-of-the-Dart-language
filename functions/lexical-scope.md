# 어휘 범위

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:red;">Dart</mark>는 **어휘 범위(Lexically scoped)**가 지정된 언어입니다. 즉, 변수의 범위는 단순히 **코드 레이아웃(코드 블록)**에 의해 정적으로 결정됩니다. 변수가 어떤 범위 내에 있는지 확인하기 위해서 <mark style="color:green;">`{}`</mark> 밖으로 코드를 따라가면 확인할 수 있습니다. 다음은 중첩 함수의 예제입니다.

```dart
String topLevel = "topLevel";

void main() {
  String insideMain = "insideMain";

  // Error: Method not found: 'myFunction'.
  // myFunction();

  void myFunction() {
    String insideFunction = "insideFunction";

    void nestedFunction() {
      String insideNestedFunction = "insideNestedFunction";

      print(topLevel);
      print(insideMain);
      print(insideFunction);
      print(insideNestedFunction);
    }

    nestedFunction();
  }

  myFunction();

  // Error: Method not found: 'nestedFunction'.
  // nestedFunction();
}
```

{% embed url="https://dartpad.dev/?id=722e03027a4900dfd846ff0a44a6f51e" %}

중첩된 어휘 범위에서 변수명이 중복될 경우 **변수 쉐도잉(Shadowing)** 발생합니다. 쉐도잉이란 안쪽 어휘 범위에서 언된 변수에 의해서 바깥쪽에 선언된 변수가 가려지는 것을 의미합니다. 중첩된 어휘 범위에서 무의식적으로 같은 이름의 변수명을 사용할 경우 변수 쉐도잉에 의해서 프로그램이 의도치 않게 동작할 수 있으므로 주의가 필요합니다.

```dart
int num = 5;

void main() {
  int delta = 1;
  for (int num = 0; num < 5; num++) {
    // 최상위 변수 num은 for문의 지역 변수 num에 가려집니다.
    print(num + delta);
  }

  // 최상위 변수 num은 함수 매개변수 num에 가려집니다.
  final sayNum = (num) => print(num);
  sayNum(10);
}
```

{% embed url="https://dartpad.dev/?id=5c32c7965f9710d555bdf4ec3b137b35" %}
