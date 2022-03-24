# 객체의 타입 확인

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

런타임에 객체의 타입을 확인하려면 [Type](https://api.dart.dev/stable/2.16.2/dart-core/Type-class.html) 객체를 반환하는 <mark style="color:green;">`Object`</mark> 클래스의 <mark style="color:green;">`runtimeType`</mark> 속성을 사용합니다.

```dart
class ImmutablePoint {
  final int x;
  final int y;
  
  const ImmutablePoint(this.x, this.y);
}

void main() {
  var a = const ImmutablePoint(1, 1);
  print('The type of a is ${a.runtimeType}');
}
```

{% embed url="https://dartpad.dev/?id=7509799becd6f973cf7e8249ac85807f" %}

<mark style="color:green;">`runtimeType`</mark> 속성 대신 [타입 테스트 연산자](https://dart.dev/guides/language/language-tour#type-test-operators)를 이용해 객체의 유형을 검사하세요.  프로덕션 환경에서 <mark style="color:green;">`object is Type`</mark> 검사 <mark style="color:green;">`object.runtimeType == Type`</mark> 검사보다 더 안정적입니다.

```dart
class ImmutablePoint {
  final int x;
  final int y;
  
  const ImmutablePoint(this.x, this.y);
}

void main() {
  var a = ImmutablePoint(1, 1);
  print('a is ImmutablePoint? ${a is ImmutablePoint}');
  
  dynamic b = ImmutablePoint(2, 3);
  if (b is ImmutablePoint) {
    print('b.x=${(b as ImmutablePoint).x}, b.y=${(b as ImmutablePoint).y}');
  }
}
```

{% embed url="https://dartpad.dev/?id=72c0b1ce265931d24f1ab1ad86577432" %}
