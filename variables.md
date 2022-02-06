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

### 기본값

Nullable 타입의 기본값(Default value)은 <mark style="color:green;">`null`</mark>입니다. 숫자를 포함 Dart의 모든 것은 객체이므로 nullable 정수 타입도 초기값은 <mark style="color:green;">`null`</mark>을 갖습니다.

```dart
int? lineCount;
assert(lineCount == null);
```

{% hint style="info" %}
프로덕션 모드에서 assert() 호출은 무시됩니다. 개발 모드에서는 <mark style="color:green;">`assert(condition)`</mark>의 <mark style="color:green;">`condition`</mark>이 <mark style="color:green;">`false`</mark>이면 예외를 던집니다. 보다 자세한 내용은 [여기](https://dart.dev/guides/language/language-tour#assert)를 참고해주세요.
{% endhint %}

Null safety를 사용할 때 non-nullable 변수는 반드시 초기화 후에 사용해야 합니다.

```dart
int lineCount = 0;
```

지역 변수는 선언 지점에 초기화할 필요는 없지만, 반드시 초기화 후에 사용해야 합니다. 예를 들어, 아래 예제에서 컴파일러는 <mark style="color:green;">`lineCount`</mark>가 <mark style="color:green;">`print()`</mark> 함수에 전달될 때 반드시 초기화된다는 사실을 알 수 있어서 정상적으로 컴파일 및 실행이 됩니다.

```dart
import 'dart:convert';

String poemFlower = """꽃 - 김춘수

내가 그의 이름을 불러주기 전에는
그는 다만
하나의 몸짓에 지나지 않았다.

내가 그의 이름을 불러주었을 때,
그는 나에게로 와서
꽃이 되었다.

내가 그의 이름을 불러준 것처럼
나의 이 빛깔과 향기에 알맞은
누가 나의 이름을 불러다오.
그에게로 가서 나도
그의 꽃이 되고 싶다.

우리들은 모두
무엇이 되고 싶다.
너는 나에게 나는 너에게
잊혀지지 않는 하나의 눈짓이 되고 싶다.
""";

void main() {
  int lineCount;
  
  // Error: Non-nullable variable 'lineCount' must be assigned before it can be used.
  // print(lineCount);

  bool weLikeToCount = true;
  if (weLikeToCount) {
    lineCount = countLines(poemFlower);
  } else {
    lineCount = 0;
  }

  // 컴파일러는 변수가 초기화 될 것을 알기 때문에 정상적으로 컴파일 됩니다.
  print(lineCount);
}

int countLines(String text) {
  return LineSplitter().convert(text).length;
}
```

최상위 변수와 클래스 변수는 게으른 초기화(Lazily initialized)를 합니다. 해당 변수들은 최초로 사용되는 시점에 초기화 됩니다.
