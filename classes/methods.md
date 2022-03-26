# 메서드

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

**메서드(Methods)**는 객체에 대한 동작을 제공하는 **함수**입니다.

#### 인스턴스 메서드

객체의 **인스턴스 메서드(Instance methods)**는 인스턴스 변수 및 <mark style="color:green;">`this`</mark>에 접근할 수 있습니다. 아래 코드에서 <mark style="color:green;">`distanceTo()`</mark> 메서드는 인스턴스 메서드의 예입니다.

```dart
import 'dart:math';

class Point {
  double x = 0;
  double y = 0;

  Point(this.x, this.y);

  double distanceTo(Point other) {
    var dx = x - other.x;
    var dy = y - other.y;
    return sqrt(dx * dx + dy * dy);
  }
}
```

#### 연산자

**연산자(Operators)**는 특별한 이름을 갖는 인스턴스 메서드입니다. <mark style="color:red;">Dart</mark>에서는 아래 이름으로 연산자를 정의할 수 있습니다.

| <mark style="color:green;">`<`</mark>  | <mark style="color:green;">`+`</mark>  | <mark style="color:green;">`\|`</mark> | <mark style="color:green;">`>>>`</mark> |   |
| -------------------------------------- | -------------------------------------- | -------------------------------------- | --------------------------------------- | - |
| <mark style="color:green;">`>`</mark>  | <mark style="color:green;">`/`</mark>  | <mark style="color:green;">`^`</mark>  | <mark style="color:green;">`[]`</mark>  |   |
| <mark style="color:green;">`<=`</mark> | <mark style="color:green;">`~/`</mark> | <mark style="color:green;">`&`</mark>  | <mark style="color:green;">`[]=`</mark> |   |
| <mark style="color:green;">`>=`</mark> | <mark style="color:green;">`*`</mark>  | <mark style="color:green;">`<<`</mark> | <mark style="color:green;">`~`</mark>   |   |
| <mark style="color:green;">`-`</mark>  | <mark style="color:green;">`%`</mark>  | <mark style="color:green;">`>>`</mark> | <mark style="color:green;">`==`</mark>  |   |

연산자 <mark style="color:green;">`==`</mark>만 존재하고 <mark style="color:green;">`!=`</mark>는 존재하지 않는 것을 볼 수 있는데, <mark style="color:green;">`!=`</mark>은 **syntactic sugar**이기 때문입니다. 예를 들어, <mark style="color:green;">`e1 != e2`</mark>는 <mark style="color:green;">`!(e1 == e2)`</mark>의 **syntactic sugar**입니다.

연산자는 <mark style="color:green;">`operator`</mark> 식별자를 이용해 선언합니다. 아래 코드는 벡터의 더하기(<mark style="color:green;">`+`</mark>), 빼기(<mark style="color:green;">`-`</mark>)를 정의합니다.

```dart
class Vector {
  final int x, y;

  Vector(this.x, this.y);

  Vector operator +(Vector v) => Vector(x + v.x, y + v.y);
  Vector operator -(Vector v) => Vector(x - v.x, y - v.y);

  bool operator ==(other) =>
      other is Vector &&
      x == other.x &&
      y == other.y;

  int get hashCode => "$x,$y".hashCode;
}

void main() {
  final v = Vector(2, 3);
  final w = Vector(2, 2);

  print("v + w == Vector(4, 5) ? ${v + w == Vector(4, 5)}");
  print("v - w == Vector(0, 1) ? ${v - w == Vector(0, 1)}");
}
```

{% embed url="https://dartpad.dev/?id=aaa8ed2d9b63dfa43fc5a53ae05c2623" %}

#### Getter와 Setter

**Getter**와 **Setter**는 객체의 속성에 대한 읽기와 쓰기 접근을 제공하는 특수한 메서드입니다. 각 인스턴스 변수에는 암시적 **getter**와 적절한 경우 **setter**가 존재합니다. <mark style="color:green;">`get`</mark>과 <mark style="color:green;">`set`</mark> 키워드를 사용하여 **getter** 및 **setter**를 구현하는 방법으로 추가 속성을 만들 수 있습니다.

아래 코드는 두개의 연산된 속성 <mark style="color:green;">`right`</mark>과 <mark style="color:green;">`bottom`</mark>을 정의합니다.

```dart
class Rectangle {
  double left, top, width, height;

  Rectangle(this.left, this.top, this.width, this.height);

  double get right => left + width;
  set right(double value) => left = value - width;
  double get bottom => top + height;
  set bottom(double value) => top = value - height;
}

void main() {
  var rect = Rectangle(3, 4, 20, 15);
  print("rect.left == 3 ? ${rect.left == 3}");
  rect.right = 12;
  print("rect.left == -8 ? ${rect.left == -8}");
}
```

{% embed url="https://dartpad.dev/?id=24f2700bdbece8765471f313cb17d80d" %}

**Getter**와 **setter**를 사용하면 클라이언트 코드를 변경하지 않고 인스턴스 변수로 시작하여 후에 메서드로 변경할 수 있습니다.

```dart
double get right => left + width;

// 위와 동일한 코드
double get right {
  return left + width;
}
```
