# 키워드

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:red;">Dart</mark> 언어는 아래와 같은 키워드를 갖습니다.

| [abstract](https://dart.dev/guides/language/language-tour#abstract-classes) _(2)_         | [else](https://dart.dev/guides/language/language-tour#if-and-else)                            | [import](https://dart.dev/guides/language/language-tour#using-libraries) _(2)_                       | [show](https://dart.dev/guides/language/language-tour#importing-only-part-of-a-library) _(1)_ |
| ----------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| [as](https://dart.dev/guides/language/language-tour#type-test-operators) (2)              | [enum](https://dart.dev/guides/language/language-tour#enumerated-types)                       | [in](https://dart.dev/guides/language/language-tour#for-loops)                                       | [static](https://dart.dev/guides/language/language-tour#class-variables-and-methods) _(2)_    |
| [assert](https://dart.dev/guides/language/language-tour#assert)                           | [export](https://dart.dev/guides/libraries/create-library-packages) _(2)_                     | [interface](https://dart.dev/guides/language/language-tour#implicit-interfaces) _(2)_                | [super](https://dart.dev/guides/language/language-tour#extending-a-class)                     |
| [async](https://dart.dev/guides/language/language-tour#asynchrony-support) _(1, 3)_       | [extends](https://dart.dev/guides/language/language-tour#extending-a-class)                   | [is](https://dart.dev/guides/language/language-tour#type-test-operators)                             | [switch](https://dart.dev/guides/language/language-tour#switch-and-case)                      |
| [await](https://dart.dev/guides/language/language-tour#asynchrony-support) _(3)_          | [extension](https://dart.dev/guides/language/language-tour#extension-methods) _(2)_           | [late](https://dart.dev/guides/language/language-tour#late-variables) _(2)_                          | [sync](https://dart.dev/guides/language/language-tour#generators) _(1)_                       |
| [break](https://dart.dev/guides/language/language-tour#break-and-continue)                | [external](https://spec.dart.dev/DartLangSpecDraft.pdf#External%20Functions) _(2)_            | [library](https://dart.dev/guides/language/language-tour#libraries-and-visibility) _(2)_             | [this](https://dart.dev/guides/language/language-tour#constructors)                           |
| [case](https://dart.dev/guides/language/language-tour#switch-and-case)                    | [factory](https://dart.dev/guides/language/language-tour#factory-constructors) _(2)_          | [mixin](https://dart.dev/guides/language/language-tour#adding-features-to-a-class-mixins) _(2)_      | [throw](https://dart.dev/guides/language/language-tour#throw)                                 |
| [catch](https://dart.dev/guides/language/language-tour#catch)                             | [false](https://dart.dev/guides/language/language-tour#booleans)                              | [new](https://dart.dev/guides/language/language-tour#using-constructors)                             | [true](https://dart.dev/guides/language/language-tour#booleans)                               |
| [class](https://dart.dev/guides/language/language-tour#instance-variables)                | [final](https://dart.dev/guides/language/language-tour#final-and-const)                       | [null](https://dart.dev/guides/language/language-tour#default-value)                                 | [try](https://dart.dev/guides/language/language-tour#catch)                                   |
| [const](https://dart.dev/guides/language/language-tour#final-and-const)                   | [finally](https://dart.dev/guides/language/language-tour#finally)                             | [on](https://dart.dev/guides/language/language-tour#catch) _(1)_                                     | [typedef](https://dart.dev/guides/language/language-tour#typedefs) _(2)_                      |
| [continue](https://dart.dev/guides/language/language-tour#break-and-continue)             | [for](https://dart.dev/guides/language/language-tour#for-loops)                               | [operator](https://dart.dev/guides/language/language-tour#\_operators) _(2)_                         | [var](https://dart.dev/guides/language/language-tour#variables)                               |
| [covariant](https://dart.dev/guides/language/sound-problems#the-covariant-keyword) _(2)_  | [Function](https://dart.dev/guides/language/language-tour#functions) _(2)_                    | [part](https://dart.dev/guides/libraries/create-library-packages#organizing-a-library-package) _(2)_ | [void](https://dart.dev/guides/language/language-tour#built-in-types)                         |
| [default](https://dart.dev/guides/language/language-tour#switch-and-case)                 | [get](https://dart.dev/guides/language/language-tour#getters-and-setters) _(2)_               | [required](https://dart.dev/guides/language/language-tour#named-parameters) _(2)_                    | [while](https://dart.dev/guides/language/language-tour#while-and-do-while)                    |
| [deferred](https://dart.dev/guides/language/language-tour#lazily-loading-a-library) _(2)_ | [hide](https://dart.dev/guides/language/language-tour#importing-only-part-of-a-library) _(1)_ | [rethrow](https://dart.dev/guides/language/language-tour#catch)                                      | [with](https://dart.dev/guides/language/language-tour#adding-features-to-a-class-mixins)      |
| [do](https://dart.dev/guides/language/language-tour#while-and-do-while)                   | [if](https://dart.dev/guides/language/language-tour#if-and-else)                              | [return](https://dart.dev/guides/language/language-tour#functions)                                   | [yield](https://dart.dev/guides/language/language-tour#generators) _(3)_                      |
| [dynamic](https://dart.dev/guides/language/language-tour#important-concepts) _(2)_        | [implements](https://dart.dev/guides/language/language-tour#implicit-interfaces) _(2)_        | [set](https://dart.dev/guides/language/language-tour#getters-and-setters) _(2)_                      |                                                                                               |

키워드 중 숫자로 마킹된 키워드는 식별자로 사용할 수 있지만 코드를 읽는데 혼란을 줄 수 있으므로 사용을 피해야 합니다.

* _(1)_로 마킹한 키워드는 문맥 키워드(Contextual keywords)로 코드의 특정 위치에서만 의미가 있습니다. 이들은 어디서나 유효한 식별자로 사용할 수 있습니다.

```dart
void main() {
  // 식별자로 사용이 가능합니다.
  var async = 1;
}

// 함수 Body 앞에서 사용되어야 유효한 키워드로 동작합니다.
void foo() async {
  // 비동기 함수 내부에서도 async를 식별자로 사용할 수 있습니다.
  var async = 1;
}
```

{% embed url="https://dartpad.dev/?id=fcbb33302116d6b7e264b8bf88a87f68" %}

* _(2)_로 마킹한 키워드는 내장 식별자(Built-in Identifiers)로 코드의 대부분 위치에서 유효한 식별자 이지만 클래스, 타입명, <mark style="color:green;">`import`</mark> 접두사로 사용할 수 없습니다.

```dart
// 클래스, 타입명, import 접두사로 사용할 수 없습니다.
import 'dart:html' as typedef;
class typedef {}

// 타입 정의 구문에서 유효한 키워드로 동작합니다.
typedef Fruit = String;

void main() {
  Fruit apple = "Apple";
  
  // 코드 대부분의 위치에서 유효한 식별자로 사용할 수 있습니다.
  var import = 1;
  var typedef = 1;
}
```

{% embed url="https://dartpad.dev/?id=3e81659b571f5f4f2a7388fa55f6600a" %}

* (3)으로 마킹한 키워드는 [비동기 지원](https://dart.dev/guides/language/language-tour#asynchrony-support)을 위한 키워드입니다. <mark style="color:green;">`await, yield`</mark>는 <mark style="color:green;">`async, async*, sync*`</mark>로 표시된 함수의 본문에서 식별자로 사용할 수 없습니다.

```dart
void main() {
  // 식별자로 사용이 가능합니다.
  var await = 1;
  var yield = 2;
}

Future<void> asyncFunction() async {
  // 비동기 함수에서는 await, yield를 식별자로 사용할 수 없습니다.
  var await = 1;
  var yield = 2;
}

Stream<int> generatorFunction(int n) async* {
  // 제너레이터 함수에서도 await, yield를 식별자로 사용할 수 없습니다.
  int await = 0;
  while (await < n) yield await++;
}
```

{% embed url="https://dartpad.dev/?id=369a7323b3abb21a3b62f62a06914edf" %}

마킹되지 않은 키워드는 예약어(Reserved words)이며 식별자로 사용할 수 없습니다.
