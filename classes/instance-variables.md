# 인스턴스 변수

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

**인스턴스 변수(Instance variables)**를 선언하는 방법은 다음과 같습니다.

```dart
class Point {
  double? x; // 인스턴스 변수 x를 선언합니다. 초기값은 null입니다.
  double? y; // 인스턴스 변수 y를 선언합니다. 초기값은 null입니다.
  double z = 0; // 인스턴스 변수 z를 선언합니다. 초기값은 0입니다.
}
```

초기화하지 않은 인스턴스 변수는 <mark style="color:green;">`null`</mark> 값을 갖습니다. 모든 인스턴스 변수는 암시적으로 **getter** 메서드가 생성됩니다. 초기화하지 않은 **Non-final** 인스턴스 변수와 <mark style="color:green;">`late final`</mark> 인스턴스 변수도 암시적으로 **setter** 메서드를 생성합니다.

선언된 위치에서 **Non-late** 인스턴스 변수를 초기화하면 인스턴스가 생성될 때 값이 설정되며, 이는 생성자와 초기화 목록이 실행되기 전에 이루어 집니다.

```dart
class Point {
  double? x; // 인스턴스 변수 x를 선언합니다. 초기값은 null입니다.
  double? y; // 인스턴스 변수 y를 선언합니다. 초기값은 null입니다.
}

void main() {
  var point = Point();
  point.x = 4; // x에 대해 setter 메서드를 사용합니다.
  assert(point.x == 4); // x에 대해 getter 메서드를 사용합니다.
  assert(point.y == null); // 기본값은 null입니다.
}
```

{% embed url="https://dartpad.dev/?id=161c980e6c550275aa691e833d436324" %}

인스턴스 변수는 <mark style="color:green;">`final`</mark>로 설정할 수 잇으며, 이 경우 딱 한번만 초기화할 수 있습니다. <mark style="color:green;">`final`</mark> 및 **non-late** 인스턴스 변수는 아래의 방법으로 초기화 할 수 있습니다.

* 변수 선언 시점에 초기화
* 생성자 매개변수를 사용해 초기화
* 생성자의 초기화 목록(Initializer list)을 사용해 초기화

```dart
class ProfileMark {
  final String name;
  final DateTime start = DateTime.now(); // 선언 시 초기화합니다.

  ProfileMark(this.name); // 생성자 매개변수를 사용해 초기화합니다.
  ProfileMark.unnamed() : name = ''; // 생성자 초기화 목록을 사용해 초기화합니다.
}
```

만약 생성자 바디에서 <mark style="color:green;">`final`</mark>로 선언된 인스턴스 변수에 값을 할당해야하는 경우 다음 중 하나의 방법을 사용하세요.

* **팩토리 생성자(Factory constructor)**를 사용
* <mark style="color:green;">`late final`</mark>을 사용
