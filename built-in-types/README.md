# 내장 타입

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:red;">Dart</mark> 언어에서는 아래 타입들을 특별하게 지원합니다.

* [Number](https://dart.dev/guides/language/language-tour#numbers) (<mark style="color:green;">`int, double`</mark>)
* [Strings](https://dart.dev/guides/language/language-tour#strings) (<mark style="color:green;">`String`</mark>)
* [Booleans](https://dart.dev/guides/language/language-tour#booleans) (<mark style="color:green;">`bool`</mark>)
* [Lists](https://dart.dev/guides/language/language-tour#lists) (<mark style="color:green;">`List`</mark>, 배열이라고도 불림)
* [Sets](https://dart.dev/guides/language/language-tour#sets) (<mark style="color:green;">`Set`</mark>)
* [Maps](https://dart.dev/guides/language/language-tour#maps) (<mark style="color:green;">`Map`</mark>)
* [Runes](https://dart.dev/guides/language/language-tour#characters) (<mark style="color:green;">`Runes`</mark>)
* [Symbol](https://dart.dev/guides/language/language-tour#symbols) (<mark style="color:green;">`Symbol`</mark>)
* null 값 (<mark style="color:green;">`Null`</mark>)

지원 내용에는 리터럴을 사용해서 객체를 생성하는 기능이 포함됩니다. 예를 들어 <mark style="color:green;">`'이것은 문자열입니다.'`</mark>는 문자열 리터럴이고 <mark style="color:green;">`true`</mark>는 부울 리터럴입니다. <mark style="color:red;">Dart</mark>의 모든 변수는 객체. 즉, 클래스의 인스턴스이기 때문에 생성자를 사용하여 변수를 초기화할 수 있습니다. 예를들어, <mark style="color:green;">`Map()`</mark> 생성자를 사용해서 <mark style="color:green;">`Map`</mark> 인스턴스를 생성할 수 있습니다.

일부 다른 타입도 <mark style="color:red;">`Dart`</mark> 언어에서 특별한 역할을 합니다.

* <mark style="color:green;">`Object`</mark> : <mark style="color:green;">`Null`</mark>을 제외한 모든 <mark style="color:red;">Dart</mark> 클래스의 수퍼 클래스(Superclass)입니다.
* <mark style="color:green;">`Future`</mark>와 <mark style="color:green;">`Stream`</mark> : [비동기 지원](https://dart.dev/guides/language/language-tour#asynchrony-support)에서 사용합니다.
* <mark style="color:green;">`Iterable`</mark> : [for-in 루프](https://dart.dev/guides/libraries/library-tour#iteration)와 동기 [제너레이터 함수](https://dart.dev/guides/language/language-tour#generator)에서 사용합니다.
* <mark style="color:green;">`Never`</mark> : 표현식이 정상적으로 평가(Evaluating)될 수 없음을 나타냅니다. 항상 예외를 <mark style="color:green;">`throw`</mark>하는 함수에서 자주 사용합니다.
* <mark style="color:green;">`dynamic`</mark> : 정적 타입 검사를 비활성화 함을 나타냅니다. 대개 <mark style="color:green;">`Object, Object?`</mark>를 대신 사용해야합니다.
* <mark style="color:green;">`void`</mark> : 값이 사용되지 않음을 나타냅니다. 주로 함수 반환값으로 사용합니다.

```dart
void main() {
  // 반환값을 지정하지 않으면 null값을 반환합니다.
  print(nullFunction());
  
  // 반환값이 void로 지정된 함수의 반환값을 사용하려고 시도하면 컴파일 에러가 발생합니다.
  // Error: This expression has type 'void' and can't be used.
  //print(voidFunction());
  
  // 정상적으로 컴파일됩니다.
  intShorthandFunction();
}

nullFunction() {}

void voidFunction() {}

// 반환값을 void로 지정했으므로 return을 시도하면 컴파일 에러가 발생합니다.
// Error: Can't return a value from a void function.
void intFunction() {
  //return 99;
}

// 단축 함수 표현식에서는 void로 반환값을 지정해도 에러가 발생하지 않습니다.
void intShorthandFunction() => 99;
```

{% embed url="https://dartpad.dev/?id=c83fea45dfd9df5b86bc885703cfe19a" %}
