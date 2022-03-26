# 열거형

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

**열거형(Enumerated types)**은 고정된 수의 상수 값을 나타내는 데 사용되는 **특별한 종류의 클래스**입니다.

#### 열거형 사용

열거형은 <mark style="color:green;">`enum`</mark> 키워드를 이용해 선언하며, 후행 쉼표를 사용할 수 있습니다.

```dart
enum Color { red, green, blue }

enum Color {
  red,
  green,
  blue,
}
```

열거형의 각 값에는 0부터 시작하는 위치를 반환하는 <mark style="color:green;">`index`</mark> **getter**가 있습니다.

```dart
assert(Color.red.index == 0);
assert(Color.green.index == 1);
assert(Color.blue.index == 2);
```

열거형의 모든 값의 목록을 얻으려면 열거형의 <mark style="color:green;">`values`</mark> 상수를 사용하세요.

```dart
List<Color> colors = Color.values;
assert(colors[2] == Color.blue);
```

열거형에는 다음과 같은 제한이 있습니다.

* 열거형은 상속, 믹스인, 인터페이스 구현에 사용될 수 없습니다.
* 열거형을 명시적으로 인스턴스화할 수 없습니다.

#### 열거형 확장

열거형에 추가적인 기능이 필요한 경우 <mark style="color:green;">`extension`</mark> 키워드를 이용해 기능을 확장한 수 있습니다.

```dart
enum Color { red, green, blue }

extension ColorExtension on Color {
  String get code {
    switch(this) {
      case Color.red:
        return "#ff0000";
      case Color.green:
        return "#00ff00";
      case Color.blue:
        return "#0000ff";
    }
  }
  
  void paintColor() {
    print("Paint it ${this.code}.");
  }
}

void main() {
  Color.blue.paintColor();
}
```

{% embed url="https://dartpad.dev/?id=ab0c416ddd058bb39874ef980c735bc5" %}
