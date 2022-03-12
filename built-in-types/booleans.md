# Boolean

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:red;">Dart</mark>에서 부울 값을 나타내기 위해서 <mark style="color:green;">`bool`</mark> 타입을 제공합니다. <mark style="color:green;">`bool`</mark> 타입은 오직 <mark style="color:green;">`true`</mark>와 <mark style="color:green;">`false`</mark> 2개의 객체만 갖으며, 둘 다 컴파일 타임 상수입니다.

<mark style="color:red;">Dart</mark>의 타입 안전성은 <mark style="color:red;">JavaScript</mark>와 달리 <mark style="color:green;">`if(truthy)`</mark> 또는 <mark style="color:green;">`asset(truthy)`</mark> 같은 코드를 사용할 수 없음을 이야기합니다.

```dart
void main() {
  var fullName = '';
  assert(fullName.isEmpty);

  var hitPoints = 0;
  assert(hitPoints <= 0);

  var unicorn;
  assert(unicorn == null);

  var iMeantToDoThis = 0 / 0;
  assert(iMeantToDoThis.isNaN);
}
```

{% embed url="https://dartpad.dev/?id=d634318130882f25a04bf135c84cd9a8" %}
