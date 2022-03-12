# 숫자 타입

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:red;">Dart</mark> 언어의 숫자 타입은 두 개의 타입으로 제공됩니다.

<mark style="color:green;">`int`</mark>\
[플랫폼 및 아키텍처에 따라 다르지만](https://dart.dev/guides/language/numbers), 64비트 이하의 정수값을 갖습니다.

<mark style="color:green;">`double`</mark>\ <mark style="color:green;">``</mark>[IEEE 754](https://ko.wikipedia.org/wiki/IEEE\_754) 표준에서 지정 64비트 부동 소수점(실수) 수입니다.

<mark style="color:green;">`int`</mark> 및 <mark style="color:green;">`double`</mark>은 모두 [num](https://api.dart.dev/stable/2.16.1/dart-core/num-class.html) 타입의 하위 클래스입니다. <mark style="color:green;">`num`</mark> 타입에는 기본적인 산술 연산자(+, -, /, \*, % 등) 대한 메서드와 기본적인 수치 연산 함수, 비트 연산 함수 등이 정의되어 있습니다. <mark style="color:green;">`num`</mark> 타입에서 찾을 수 없는 수치 연산  기능은 [dart:math](https://api.dart.dev/stable/2.16.1/dart-math/dart-math-library.html) 라이브러리에서 제공됩니다.

아래 코드는 정수 및 실수 리터럴을 정의하는 방법입니다.

```dart
// 정수 리터럴을 정의하는 방법입니다.
var x = 1; // 10진수 표현식
var hex = 0xDEADBEEF; // 16진수 표현식
var exponent = 8e5; // 정수 지수 표현식

// 실수 리터럴을 정의하는 방법입니다.
var y = 1.1; // 실수 표현식
var exponents = 1.42e5; // 실수 지수 표현식
```

{% embed url="https://dartpad.dev/?id=a3fec145fa02eb156115000058885277" %}

<mark style="color:green;">`num`</mark> 타입을 이용하면 <mark style="color:green;">`int`</mark>와 <mark style="color:green;">`double`</mark>을 모두 할당할 수 있는 변수를 선언할 수 있습니다. 정수 리터럴을 <mark style="color:green;">`double`</mark> 타입 변수에 할당하면 자동으로 타입 변환이 이루어집니다.

```dart
void main() {
  // x는 int와 double 모두를 할당할 수 있습니다.
  num x = 1;
  x += 2.5;
  
  // 1은 자동으로 1.0으로 변환됩니다.
  double z = 1;
}
```

{% embed url="https://dartpad.dev/?id=51629f5a0d46bb9dcb3c1413889f39fb" %}

<mark style="color:red;">Dart</mark> 언어에서는 문자열과 숫자를 상호 변환하는 방법을 제공합니다.

```dart
void main() {
  // String -> int
  var one = int.parse('1');
  assert(one == 1);

  // String -> double
  var onePointOne = double.parse('1.1');
  assert(onePointOne == 1.1);

  // int -> String
  String oneAsString = 1.toString();
  assert(oneAsString == '1');

  // double -> String
  String piAsString = 3.14159.toStringAsFixed(2);
  assert(piAsString == '3.14');
}
```

{% embed url="https://dartpad.dev/?id=e89fde5cf59f80d5e79032fbdd59142e" %}

<mark style="color:green;">`int`</mark> 타입은 비트 필드에서 플래그를 조작하고 마스킹하는데 유용한 shift(<mark style="color:green;">`<<, >>`</mark>), complement(<mark style="color:green;">`~`</mark>), AND(<mark style="color:green;">`&`</mark>), OR(<mark style="color:green;">`|`</mark>), XOR(<mark style="color:green;">`^`</mark>) 같은 비트 연산을 지원합니다. 보다 자세한 내용은 [여기](https://dart.dev/guides/language/language-tour#bitwise-and-shift-operators)를 참고해주세요.

```dart
void main() {
  // 0011 << 1 == 0110
  assert((3 << 1) == 6);
  
  // 0011 | 0100 == 0111
  assert((3 | 4) == 7);
  
  // 0011 & 0100 == 0000
  assert((3 & 4) == 0);
}
```

{% embed url="https://dartpad.dev/?id=cc08f8608191c95575e2cb8e472156df" %}

숫자 리터럴은 컴파일 타입 상수입니다. 컴파일 타임 상수로만 이루어진 산술 표현식의 평가 결과는 상수로 사용할 수 있습니다.

```dart
void main() {
  const msPerSecond = 1000;
  const secondsUntilRetry = 5;
  const msUntilRetry = secondsUntilRetry * msPerSecond;
}
```

{% embed url="https://dartpad.dev/?id=b3bb745f583ed14516eb3b3cdf22e9d0" %}
