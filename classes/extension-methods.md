# 확장 메서드

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

**확장 메서드(Extension methods)**는 기존 라이브러리에 기능을 추가하는 방법입니다. 정의된 확장 메서드는 원래 타입에 제공했던 기능인것 처럼 동작합니다.

확장 메서드는 <mark style="color:green;">`extension ExtensionType on TargetType { ... }`</mark>형태로 정의합니다. 보다 자세한 내용은 [여기](https://dart.dev/guides/language/extension-methods)를 참고해주세요.

```dart
class Person {
  final String _name;

  Person(this._name);
}

extension PersionExtension on Person {
  String greet(String who) => 'Hello, $who. I am $_name.';
}

void main() {
  final bob = Person('Kathy');
  print(bob.greet("Bob"));
}
```

{% embed url="https://dartpad.dev/?id=f4bbb71e5e0ef206457c48c78ce3ab17" %}
