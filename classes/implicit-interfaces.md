# 암시적 인터페이스

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

**모든 클래스는** 클래스의 모든 멤버와 구현하는 모든 인터페이스를 포함하는 인터페이스를 암시적으로 정의합니다. 만약 클래스 B의 구현을 상속하지 않고 클래스 B의 API를 지원하는 A 클래스를 생성하려면 클래스 A가 인터페이스 B를 구현해야 합니다.

클래스는 하나 이상의 인터페이스를 <mark style="color:green;">`implements`</mark> 절에 선언한 다음 인터페이스에 필요한 **API**를 구현합니다.

```dart
// Person 클래스는 암시적 인터페이스인 greet() 메서드를 갖습니다.
class Person {
  // 인터페이스에 있지만, 이 라이브러리에서만 접근 가능합니다.
  final String _name;

  // 생성자는 인터페이스에 존재하지 않습니다.
  Person(this._name);

  String greet(String who) => 'Hello, $who. I am $_name.';
}

// Person 인터페이스를 구현합니다.
class Impostor implements Person {
  // Error: The non-abstract class 'Impostor' is missing implementations for these members: - Person._name
  String get _name => '';

  String greet(String who) => 'Hi $who. Do you know who I am?';
}

String greetBob(Person person) => person.greet('Bob');

void main() {
  print(greetBob(Person('Kathy')));
  print(greetBob(Impostor()));
}
```

{% embed url="https://dartpad.dev/?id=9d576e849a921ec86d31a7598539ed0b" %}

아래 코드는 여러 인터페이스를 구현하는 예입니다.

```dart
class Point implements Comparable, Location {...}
```
