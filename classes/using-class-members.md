# 클래스 멤버 사용하기

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

객체는 함수(멤버 메서드)와 데이터(멤버 변수)로 구성된 멤버가 있습니다. 객체에 점(<mark style="color:green;">`.`</mark>)을 이용해 멤버에 접근하 메서드는 해당 객체의 함수와 데이터에 접근할 수 있습니다. 객체가 Nullable인 경우 예외를 방지하기 위해서 <mark style="color:green;">`?.`</mark> 연산자를 사용하세요.

```dart
import "dart:math";

void main() {
  final p1 = Point(2, 2);
  print("(x=${p1.x}, y=${p1.y})");
  
  // Nullable point 객체
  Point? p2 = null;
  
  // Null 가능성이 있는 객체의 멤버를 안전하게 사용하려면 ?. 연산자를 사용하세요.
  final distance = p2?.distanceTo(p1);
  print("distance=$distance");
}
```

{% embed url="https://dartpad.dev/?id=838da4fe932123f1127ee35c546ce05d" %}
