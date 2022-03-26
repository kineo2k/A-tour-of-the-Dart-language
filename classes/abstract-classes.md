# 추상 클래스

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:green;">`abstract`</mark> 키워드를 이용해 인스턴스화 할 수 없는 클래스인 **추상 클래스(Abstract Class)**를 정의할 수 있습니다. 추상 클래스는 일부 구현과 함께 인터페이스를 정의하는데 유용 합니다. 추상 클래스는 추상 메서드를 포함할 수 있습니다.

```dart
// 추상 클래스는 인스턴스화 할 수 없습니다.
abstract class AbstractContainer {
  // 생성자, 필드, 메서드를 정의할 수 있습니다.

  // 추상 메서드를 포함할 수 있습니다.
  void updateChildren();
}
```

추상 클래스에서 **팩터리 생성자**를 제공하여 추상 클래스의 기본 구현을 제공할 수 습니다. 대표적으로 <mark style="color:red;">Dart</mark>의 [Map](https://api.dart.dev/stable/2.16.1/dart-core/Map-class.html)은 추상 클래스이면서 인스턴스를 생성할 수 있도록 제공하고 있습니다. 내부적으로는 빈 [LinkedHashMap](https://api.dart.dev/stable/2.16.1/dart-collection/LinkedHashMap-class.html) 인스턴스를 생성합니다.

```dart
part of dart.core;

abstract class Map<K, V> {
  external factory Map();
  
  ...
}
```
