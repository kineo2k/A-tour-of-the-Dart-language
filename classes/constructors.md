# 생성자

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

클래스명과 동일한 이름의 함수로 생성자를 선언합니다. <mark style="color:green;">`this`</mark> 키워드는 현재 인스턴스를 나타냅니다. <mark style="color:green;">`this`</mark> 키워드는 이름 충돌이 발생하는 경우에만 사용하고 그렇지 않으면 <mark style="color:red;">Dart</mark> 스타일에서는 생략합니다.

```dart
class Point {
  double x = 0;
  double y = 0;

  Point(double x, double y) {
    this.x = x;
    this.y = y;
  }
}
```

인스턴스 변수에 생성자 인수를 할당하는 패턴은 매우 일반적이며, <mark style="color:red;">Dart</mark>는 이를 쉽게해주는 [Syntactic sugar](https://en.wikipedia.org/wiki/Syntactic\_sugar)를 제공합니다.

```dart
class Point {
  double x = 0;
  double y = 0;

  // 생성자 바디가 실행되기 전에 x, y변수를 설정해 주는 Syntactic sugar입니다.
  Point(this.x, this.y);
}
```

#### 기본 생성자

생성자를 선언하지 않으면 암시적으로 **기본 생성자(Default constructors)**가 제공됩니다. 기본 생성자는 인수가 없으며 슈퍼 클래스의 인수가 없는 생성자를 자동으로 호출합니다. 생성자를 별도로 선언할 경우 기본 생성자는 제공되지 않습니다.

#### 생성자는 상속되지 않습니다.

서브 클래스는 슈퍼 클래스에서 생성자를 상속하지 않습니다. 생자를 선언하지 않는 서브 클래스에는 기본 생성자만 있습니다.

#### 명명된 생성자

**명명된 생성자(Named constructors)**를 이용해 여러 생성자를 구현하거나 추가적인 **명확성**을 제공합니다.

```dart
const double xOrigin = 0;
const double yOrigin = 0;

class Point {
  double x = 0;
  double y = 0;

  Point(this.x, this.y);

  // 명명된 생성자
  Point.origin()
      : x = xOrigin,
        y = yOrigin;
}
```

생성자는 상속되지 않기 때문에 슈퍼 클래스에 정의된 명명된 생성자로 서브 클래스를 생성하려면 서브 클래스에서 해당 생성자를 구현해야 합니다.

#### 기본이 아닌 슈퍼 클래스 생성자 호출

기본적으로 서브 클래스의 생성자는 슈퍼 클래스의 기본 생성자를 자동으로 호출합니다. 슈퍼 클래스의 생성자는 생성자 본문의 시작 부분에서 호출됩다. **초기화 목록(Initializer list)**을 사용하는 경우에는 슈퍼 클래스의 생성자가 호출되기 전 에 초기화 목록이 실행됩니다.

1. 초기화 목록 실행
2. 슈퍼 클래스의 인수가 없는 생성자 실행
3. 기본 클래스의 인수가 없는 생성자 실행

슈퍼 클래스에 기본 생성자가 없는 경우 슈퍼 클래스의 생성자 중 하나를 수동으로 호출해야 합니다. 생성자 선언 뒤에 <mark style="color:green;">`:`</mark>을 입력하고 슈퍼 클래스 생성자를 지정할 수 있습니다.

```dart
class Person {
  String? firstName;

  Person.fromJson(Map data) {
    print('in Person');
  }
}

class Employee extends Person {
  // Person 클래스는 기본 생성자가 없으므로 반드시 super.fromJson(data)를 호출해야 합니다.
  Employee.fromJson(Map data) : super.fromJson(data) {
    print('in Employee');
  }
  
  // 생성자 바디에서 슈퍼 클래스 생성자를 호출하는 방법은 지원하지 않습니다.
  // Employee.fromJson(Map data) {
  //   super.fromJson(data);
  // }
}

void main() {
  var employee = Employee.fromJson({});
  print(employee);
}

<출력결과>
in Person
in Employee
Instance of 'Employee'
```

{% embed url="https://dartpad.dev/?id=1096fb3ecc573f5b004d3ad4e10f5607" %}

슈퍼 클래스 생성자에 대한 인수는 생성자를 호출하기 전에 평가되기 때문에 슈퍼 클래스 생성자의 인수는 함수 호출과 같은 표현식도 가능합니다.

```dart
class Employee extends Person {
  Employee() : super.fromJson(fetchDefaultData());
}
```

슈퍼 클래스 생성자에 대한 인수는 <mark style="color:green;">`this`</mark>에 접근할 수 없습니다. 그래서 인자의 표현식은 <mark style="color:green;">`static`</mark> 메서드를 사용할 수 있지만 인스턴스 메서드는 사용할 수 없습니다.

#### 초기화 목록

생성자 선언 뒤에 슈퍼 클래스 생성자를 호출하는 것 외에도 **초기화 목록(Initializer list)**을 선언할 수 있으며, 생성자 본문이 실행되기 전에 인스턴스 변수를 초기화할 수 있습니다.

```dart
Point.fromJson(Map<String, double> json)
    : x = json['x']!,
      y = json['y']! {
  print('In Point.fromJson(): ($x, $y)');
}
```

개발 중인 상태에서는 <mark style="color:green;">`assert`</mark>를 사용해 생성자 인자의 유효성을 검증할 수도 있습니다.

```dart
Point.withAssert(this.x, this.y) : assert(x >= 0) {
  print('In Point.withAssert(): ($x, $y)');
}
```

초기화 목록은 <mark style="color:green;">`final`</mark> 인스턴스 변수를 초기화 할때 유용합니다.

```dart
import 'dart:math';

class Point {
  final double x;
  final double y;
  final double distanceFromOrigin;

  // 초기화 목록을 사용해 3개의 final 인스턴스 변수를 초기화 합니다.
  Point(double x, double y)
      : x = x,
        y = y,
        distanceFromOrigin = sqrt(x * x + y * y);
}

void main() {
  var p = Point(2, 3);
  print(p.distanceFromOrigin);
}
```

{% embed url="https://dartpad.dev/?id=b5a441665d13579dfd1b46bebc708bf1" %}

#### 생성자 리디렉션

가끔은 생성자의 목적이 같은 클래스의 다른 생성자를 호출하는 것일수 있습니다. 생성자 리디렉션은 생성자 선언 뒤에 <mark style="color:green;">`:`</mark>을 붙이고 <mark style="color:green;">`this`</mark> 키워드를 이용해 인자를 넘기는 형태로 다른 생성자를 호출합니다.

```dart
class Point {
  double x, y;

  // 메인 생성자입니다.
  Point(this.x, this.y);

  // 메인 생성자에 위임합니다.
  Point.alongXAxis(double x) : this(x, 0);
}
```

#### 상수 생성자

클래스가 **불변(Immutability) 객체**를 생성하는 경우 이 객체를 컴파일 타임 상수로 만들 수 있습니다. 생성자 선언 앞에   <mark style="color:green;">`const`</mark>를 붙이고 모든 인스턴스 변수를 <mark style="color:green;">`final`</mark>로 만들면 객체를 만들 수 있습니다.

```dart
class ImmutablePoint {
  static const ImmutablePoint origin = ImmutablePoint(0, 0);

  final double x, y;

  const ImmutablePoint(this.x, this.y);
}
```

[생성자 사용](https://dart.dev/guides/language/language-tour#using-constructors)에서 살펴본 것처럼 상수 생성자를 사용해도 인스턴스 생성 시 변수로 생성했다면 컴파일 타임 상수가 아닙니다.

#### 팩터리 생성자

객체를 재사용 하는 등 항상 새 인스턴스가 필요하지 않은 상황에서는 <mark style="color:green;">`factory`</mark> 키워드를 사용하세요. 예를 들어 캐시에서 인스턴스를 반환하거나 하위 타입의 인스턴스를 반환할 수 있습니다. 팩터리 생성자의 다른 사용 사례로 초기화 목록에서 처리할 수 없는 로직을 이용해 <mark style="color:green;">`final`</mark> 변수를 초기화 할 수도 있습니다.

아래 코드의 <mark style="color:green;">`Logger`</mark> 팩터리 생성자는 캐시에서 객체를 반환하고 <mark style="color:green;">`Logger.fromJson`</mark> 팩터리 생성자는 <mark style="color:green;">`final`</mark> 변수를 초기화 합니다.

```dart
class Logger {
  final String name;
  bool mute = false;

  // _cache is library-private, thanks to
  // the _ in front of its name.
  static final Map<String, Logger> _cache = <String, Logger>{};

  factory Logger(String name) {
    return _cache.putIfAbsent(name, () => Logger._internal(name));
  }

  factory Logger.fromJson(Map<String, Object> json) {
    return Logger(json['name'].toString());
  }

  Logger._internal(this.name);

  void log(String msg) {
    if (!mute) print(msg);
  }
}

void main() {
  var logger = Logger('UI');
  logger.log('Button clicked');

  var logMap = {'name': 'UI'};
  var loggerJson = Logger.fromJson(logMap);
  
  print("logger == loggerJson ? ${identical(logger, loggerJson)}");
}
```

{% embed url="https://dartpad.dev/?id=925aae5b1b831da5618e94c1f2c86a12" %}
