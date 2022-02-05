# Dart 언어 둘러보기

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

![](.gitbook/assets/Dart.png)

## 기본적인 다트 프로그

```dart
// 함수를 정의합니다.
void printInteger(int aNumber) {
  print('The number is $aNumber.');  // 콘솔에 출력합니다.
}

// Dart 프로그램은 main 함수에서 시작합니다.
void main() {
  var number = 42; // 변수를 선언하고 초기화 합니다.
  printInteger(number); // 함수를 호출합니다.
}
```

{% embed url="https://dartpad.dev/?id=71448afab00f1b4ded8a50e3fdaa397c" %}

이 예제는 <mark style="color:red;">Dart</mark> 프로그램에 대해 많은 것을 알려줍니다.

<mark style="color:green;">`// 이건 주석입니다.`</mark>\ <mark style="color:green;">``</mark>한 줄짜리 주석입니다. 컴파일러는 <mark style="color:green;">`//`</mark>부터 줄 끝까지를 무시합니다.\
<mark style="color:green;">`/* ... */`</mark>을 이용해 여러 줄 주석을 표현합니다. 컴파일러는 <mark style="color:green;">`/*`</mark> 부터 <mark style="color:green;">`*/`</mark> 사이에 모든 내용을 무시합니다.\
문서 주석은 <mark style="color:green;">`///`</mark> 또는 <mark style="color:green;">`/**`</mark>으로 시작합니다. 보다 자세한 내용은 [여기](https://dart.dev/guides/language/effective-dart/documentation#doc-comments)를 참고하세요.

<mark style="color:green;">`void`</mark>\
반환값을 사용하지 않을 경우를 나타내는 특수한 타입입니다. <mark style="color:green;">`printInteger`</mark>와 <mark style="color:green;">`main`</mark>함수는 명시적인 반환값이 없으므로 <mark style="color:green;">`void`</mark> 반환값 타입을 갖습니다.

<mark style="color:green;">`int`</mark>\
정수 타입을 나타냅니다. <mark style="color:red;">Dart</mark> 언어는 <mark style="color:green;">`String, List, bool`</mark> 등  [기본 타입(built-in types)](https://dart.dev/guides/language/language-tour#built-in-types) 제공합니다.

<mark style="color:green;">`42`</mark>\
숫자 리터럴(Literal)입니다. 리터럴은 일종의 컴파일 타임 상수(compile-time constant)입니다.

<mark style="color:green;">`print()`</mark>\
콘솔 출력을 위해서 Dart 언어에서 제공하는 [내장 함수(built-in functions)](https://medium.com/jay-tillu/functions-in-dart-86c66b791d34) 입니다.

<mark style="color:green;">`'...'`</mark> 또는 <mark style="color:green;">`"..."`</mark>\
문자열 리터럴입니다.

<mark style="color:green;">`$변수명`</mark> 또는 <mark style="color:green;">`${표현식}`</mark>\
문자열 인터폴레이션(interpolation)입니다. 문자열 리터럴에 변수 또는 표현식 평가 결과를 삽입합니다.

<mark style="color:green;">`main()`</mark>\
Dart 프로그램 실행이 시작되는(entry point) 최상위 함수입니다. 보다 자세한 내용은 [여기](https://dart.dev/guides/language/language-tour#the-main-function)를 참고해주세요.

<mark style="color:green;">`var`</mark>\
타입을 지정하지 않고 변수를 선언하는 방법입니다. 컴파일 타임에 이 변수의 타입은 초기값 <mark style="color:green;">`42`</mark>에 의해서 <mark style="color:green;">`int`</mark> 타입으로 결정됩니다.

