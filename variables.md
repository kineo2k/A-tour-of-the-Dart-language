# 변수

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

변수는 아래와 같이 선언하고 초기화 합니다.

```dart
var name = 'Bob';
```

변수에는 객체의 참조를 저장합니다. 변수 <mark style="color:green;">`name`</mark>은 "Bob"을 값으로 갖는 <mark style="color:green;">`String`</mark> 객체를 참조합니다. 컴파일러에 의해 <mark style="color:green;">`name`</mark>은 <mark style="color:green;">`String`</mark> 타입으로 추론됩니다. 변수가 특정 타입으로 제한되지 않을 경우 <mark style="color:green;">`Object`</mark> 또는 <mark style="color:green;">`dynamic`</mark>을 사용할 수 있습니다.

```dart
Object name = 'Bob';
dynamic name = 'Bob';
```

변수 선언 시 명시적으로 타입을 지정할 수도 있습니다.

```dart
String name = 'Bob';
```
