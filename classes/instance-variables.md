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

초기화하지 않은 인스턴스 변수는 <mark style="color:green;">`null`</mark> 값을 갖습니다. 모든 인스턴스 변수는 암시적으로 **setter, getter** 메서드가 생성됩니다. 초기화하지 않은 **Non-final** 인스턴스 변수와 <mark style="color:green;">`late final`</mark> 인스턴스 변수도 암시적으로 **setter** 메서드를 생성합니다.

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
* 생성자의 **초기화 목록(Initializer list)**을 사용해 초기화

```dart
class ProfileMark {
  final String name;
  final DateTime start = DateTime.now(); // 선언 시 초기화합니다.

  ProfileMark(this.name); // 생성자 매개변수를 사용해 초기화합니다.
  ProfileMark.unnamed() : name = ''; // 생성자 초기화 목록을 사용해 초기화합니다.
}
```

만약 생성자 바디에서 <mark style="color:green;">`final`</mark>로 선언된 인스턴스 변수에 값을 할당해야하는 경우 다음 중 하나의 방법을 사용하세요.

* <mark style="color:green;">`late final`</mark>을 사용
* **팩토리 생성자(Factory constructor)**를 사용

아래 코드는 설정된 <mark style="color:green;">`x, y`</mark> 각 좌표 크기보다 2배 큰 크기로 좌표를 설정하여 점 인스턴스를 생성합니다. 클래스 바디에서 <mark style="color:green;">`x, y`</mark> 값이 2를 곱하는데 <mark style="color:green;">`x, y`</mark>는 <mark style="color:green;">`final`</mark>로 선언 되었기 때문에 **setter**가 존재하지 않고 컴파일 에러가 발생합니다.

```dart
class DoublingPoint {
  final int x;
  final int y;
  
  DoublingPoint(int x, int y) {
    // Error: The setter 'x' isn't defined for the class 'DoublingPoint'.
    this.x = x * 2;
    
    // Error: The setter 'y' isn't defined for the class 'DoublingPoint'.
    this.y = y * 2;
  }
}

void main() {
  final dp = DoublingPoint(1, 1);
  print("${dp.x}, ${dp.y}");
}
```

{% embed url="https://dartpad.dev/?id=abd97e98d6aa40079a85a08500b59c87" %}

<mark style="color:green;">`late`</mark> 키워드를 <mark style="color:green;">`final`</mark> 키워드 앞에 추가하면 **setter**가 생성되어 클래스 바디에서 <mark style="color:green;">`final`</mark> 인스턴스 변수를 초기화하는게 가능합니다. <mark style="color:green;">`late final`</mark> 인스턴스 변수는 단 한번만 초기화가 가능하기 때문에 초기화 후 추가로 값을 변경하려고 시도하면 런타임 에러를 일으킵니다.

```dart
class DoublingPoint {
  // late final 필드는 setter를 생성합니다.
  late final int x;
  late final int y;
  
  DoublingPoint(int x, int y) {
    this.x = x * 2;
    this.y = y * 2;
    
    // Uncaught Error: LateInitializationError: Field 'x' has already been initialized.
    // this.x = x * 3;
  }
}

void main() {
  final dp = DoublingPoint(1, 1);
  print("${dp.x}, ${dp.y}");
}
```

{% embed url="https://dartpad.dev/?id=7945bb5c45846e037f7e9f29114d9420" %}

<mark style="color:green;">`late final`</mark>로 선언하면 암시적으로 **setter**가 생성되므로 반드시 원하는 시점에 초기화하는 것을 잊지 말아야 합니다. 초기화 코드가 누락될 경우 해당 인스턴스를 사용하는 쪽에서 객체에 대해 의도치 않은 변경을 가할 수 있어 주의가 필요합니다.

생성자 바디에서 <mark style="color:green;">`final`</mark> 인스턴스 변수를 초기화하는 다른 방법은 **팩터리 생성자**를 사용하는 방법입니다.

```dart
class Point {
  final int x;
  final int y;
  
  // Point 클래스 내부에서만 접근 가능한 비공개 생성자 _internal을 정의합니다.
  Point._internal(this.x, this.y);
  
  // 팩터리 생성자에서 2를 곱한 값을 _internal에 전달하여 변수를 초기화합니다.
  factory Point.doubling(int x, int y) {
    return Point._internal(x * 2, y * 2);
  }
}

void main() {
  final dp = Point.doubling(1, 1);
  print("${dp.x}, ${dp.y}");
}
```

{% embed url="https://dartpad.dev/?id=712e9755984929128488711f3a86a136" %}
