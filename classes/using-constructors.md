# 생성자 사용하기

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

**생성자(Constructor)**를 사용해서 객체를 만들 수 있습니다. 생성자의 이름은 <mark style="color:green;">`ClassName`</mark>이나 <mark style="color:green;">`ClassName.identifier`</mark>를 사용할 수 있습니다. 예를 들어, 아래 코드는 <mark style="color:green;">`Point()`</mark>와 <mark style="color:green;">`Point.fromJson()`</mark> 생성자를 이용해서 <mark style="color:green;">`Point`</mark> 객체를 생성합니다.

```dart
var p1 = Point(2, 2);
var p2 = Point.fromJson({'x': 1, 'y': 2});
```

아래 코드는 위에 코드와 동일한 표현입니다. <mark style="color:red;">Dart</mark> 언어에서 생성자 이름 앞에 <mark style="color:green;">`new`</mark> 키워드를 사용하는 것은 선택 사항입니다.

```dart
var p1 = new Point(2, 2);
var p2 = new Point.fromJson({'x': 1, 'y': 2});
```

일부 클래스는 **상수 생성자(Constant constructors)**를 제공합니다. 상수 생성자를 사용하면 **컴파일 타임 상수 객체**를 생성하려면 생성자 이름 앞에 <mark style="color:green;">`const`</mark>를 붙입니다.

```dart
var p = const ImmutablePoint(2, 2);
```

두 개의 동일한 컴파일 타임 상수 객체를 구성하면 하나의 표준 인스턴스가 생성됩니다.

```dart
class ImmutablePoint {
  final int x;
  final int y;
  
  const ImmutablePoint(this.x, this.y);
}

void main() {
  var a = const ImmutablePoint(1, 1);
  var b = const ImmutablePoint(1, 1);

  // 두 객체는 같은 객체입니다.
  print("a == b ? ${identical(a, b)}");
  
  var c = ImmutablePoint(1, 1);
  var d = ImmutablePoint(1, 1);

  // 두 객체는 다른 객체입니다.
  print("c == d ? ${identical(c, d)}");
}
```

{% embed url="https://dartpad.dev/?id=5c1e55957903de5fab14797b29ec8528" %}

**상수 컨텍스트(Context)** 내에서 생성자 리터럴 앞에서 <mark style="color:green;">`const`</mark>를 생략할 수 있습니다. 아래 예제는 <mark style="color:green;">`const`</mark> 맵을 생성하는 코드인데 너무 많은 <mark style="color:green;">`const`</mark> 키워드가 사용되었습니다.

```dart
const pointAndLine = const {
  'point': const [const ImmutablePoint(0, 0)],
  'line': const [const ImmutablePoint(1, 10), const ImmutablePoint(-2, 11)],
};
```

이 경우 첫번째 <mark style="color:green;">`const`</mark> 키워드를 제외하고 모두 생략할 수 있습니다. 이때 사용된 <mark style="color:green;">`const`</mark>는 상수 컨텍스트를 생성합니다.

```dart
const pointAndLine = {
  'point': [ImmutablePoint(0, 0)],
  'line': [ImmutablePoint(1, 10), ImmutablePoint(-2, 11)],
};
```
