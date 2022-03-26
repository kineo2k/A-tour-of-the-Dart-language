# 클래스 변수와 메서드

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:green;">`static`</mark> 키워드를 이용해서 정적 변수와 메서드를 구현합니다.

#### 정적 변수

**정적 변수(Static variables)**는 클래스 상태 및 상수 정의에 사용합니다. 정적 변수는 사용되기 전까지 초기화되지 않습니다. <mark style="color:red;">Dart</mark>에서는 정적 변수에 <mark style="color:green;">`lowerCamelCase`</mark> [스타일](https://dart.dev/guides/language/effective-dart/style)이 추천됩니다.

```dart
class Queue {
  static const initialCapacity = 16;
  // ···
}

void main() {
  assert(Queue.initialCapacity == 16);
}
```

#### 정적 메서드

**정적 메서드(Static methods)**는 클래스 레벨에서 제공할 기능을 정의하며, 정적 변수와 맞찬가지로 클래스명을 이용해 접근합니다.&#x20;

```dart
import 'dart:math';

class Point {
  double x, y;
  Point(this.x, this.y);

  static double distanceBetween(Point a, Point b) {
    var dx = a.x - b.x;
    var dy = a.y - b.y;
    return sqrt(dx * dx + dy * dy);
  }
}

void main() {
  var a = Point(2, 2);
  var b = Point(4, 4);
  var distance = Point.distanceBetween(a, b);
  assert(2.8 < distance && distance < 2.9);
  print(distance);
}
```

{% embed url="https://dartpad.dev/?id=7534361a597155a731e3906af85d7fc8" %}

정적 메서드는 컴파일 타임 상수로 사용할 수 있습니다. 이를 이용해 정적 메서드를 상수 생성자에 대한 매개 변수로 전달할 수 있습니다.
