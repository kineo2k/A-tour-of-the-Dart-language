# 예외 처리

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:red;">Dart</mark>는 예외(Exception)를 던지고(Throw) 잡을 수(Catch) 있습니다. 예외는 예상하지 못한 일이 발생했음을 나타내는 오류입니다. 예외가 처리되지 않으면 예외를 발생시킨 [isolate](https://dart.dev/guides/language/language-tour#isolates)가 일시 중단되고 일반적으로 **isolate**와 해당 프로그램이 종료됩니다.

<mark style="color:red;">Java</mark>와 달리 <mark style="color:red;">Dart</mark>의 모든 예외는 **확인되지 않은 예외(Unchecked exception)**입니다. 메서드는 <mark style="color:green;">`throw`</mark>할 수 있는 예외를 선언하지 않으며 예외를 <mark style="color:green;">`catch`</mark>할 필요가 없습니다.

<mark style="color:red;">Dart</mark>는 미리 정의된 수많은 [Exception](https://api.dart.dev/stable/2.16.1/dart-core/Exception-class.html)과 [Error](https://api.dart.dev/stable/2.16.1/dart-core/Error-class.html)의 하위 타입을 제공합니다. 당연히 자신만의 예외를 정의할 수도 있습니다. <mark style="color:red;">Dart</mark> 프로그램은 **Exception** 및 **Error** 객체 뿐만아니라 모든 **Non-null 객체**를 예외로 <mark style="color:green;">`throw`</mark> 할 수 있습니다. 하지만 프로덕션 코드들은 대게 **Error**나 **Exception**을 구현한 타입을 예외로 던집니다.

#### Throw

```dart
// Exception 객체를 throw하는 예제입니다.
throw FormatException('Expected at least 1 section');

// 문자열 객체를 throw할 수도 있습니다.
throw 'Out of llamas!';
```

예외를 던지거나 발생시키는 것은 표현식(Expression)이기 때문에 <mark style="color:green;">`=>`</mark>문 뿐만 아니라 표현식을 허용하는 모든 곳에서 <mark style="color:green;">`throw`</mark>할 수 있습니다.

```dart
void distanceTo(Point other) => throw UnimplementedError(); 
```

#### Catch

예외를 잡으면 예외를 <mark style="color:green;">`rethrow`</mark>하지 않는한 예외 전파가 중지됩니다. 예외를 잡으면 예외를 처리할 수 있습니다. 예외를 잡을 때 예외 객체가 필요하지 않은 경우 <mark style="color:green;">`on`</mark>을 이용할 수 있으며, 예외 객체가 필요한 경우 <mark style="color:green;">`catch`</mark>를 사용합니다. <mark style="color:green;">`on`</mark>과 <mark style="color:green;">`catch`</mark>는 둘중 하나 또는 둘다 사용할 수 있습니다. <mark style="color:green;">`on`</mark>을 사용할 경우 Exception 타입을 명시해야하며, <mark style="color:green;">`catch`</mark>를 사용할 경우 예외를 처리하기 위해 예외 객체가 사용됩니다.

```dart
class OutOfLlamasException implements Exception {
  String cause;
  OutOfLlamasException(this.cause);
}

void main() {
  try {
    breedMoreLlamas();
  } on OutOfLlamasException {
    // 특정 Exception 타입을 catch합니다.
    buyMoreLlamas();
  } on Exception catch (e) {
    // Exception 타입의 모든 예외를 처리합니다.
    print('Unknown exception: $e');
  } catch (e) {
    // 유형을 지정하지 않고 모든 타입을 처리합니다.
    print('Something really unknown: $e');
  }
}

void breedMoreLlamas() {
  throw OutOfLlamasException("breed More Llamas!");
}

void buyMoreLlamas() {
  throw 'Out of llamas!';
}
```

{% embed url="https://dartpad.dev/?id=b52174252a4227d45f3269694abfd745" %}

<mark style="color:green;">`catch()`</mark>에는 하나 또는 두 개의 매개변수를 지정할 수 있습니다. 첫 번째는 <mark style="color:green;">`throw`</mark>된 예외 객체이고, 두 번째는 [StackTrace](https://api.dart.dev/stable/2.16.1/dart-core/StackTrace-class.html) 객체입니다. 예외를 계속적으로 전파하면서 부분적으로 예외를 처리하려면 <mark style="color:green;">`rethrow`</mark> 키워드를 사용합니다.

```dart
void misbehave() {
  try {
    dynamic foo = true;

    // 런타임 에러 발생
    print(foo++);
  } catch (e) {
    print('misbehave() partially handled ${e.runtimeType}.');

    // 예외를 계속 전파시켜서 호출자 쪽에서 예외를 확인할 수 있도록 합니다.
    rethrow;
  }
}

void main() {
  try {
    misbehave();
  } catch (e, s) {
    // 예외 내용과 StackTrace를 함께 출력합니다.
    print('main() finished handling ${e.runtimeType}.\n$s');
  }
}
```

{% embed url="https://dartpad.dev/?id=45197e249209e3e2c6db4a2e3871d861" %}

#### Finally

예외 발생여부와 무관하게 일 코드가 항상 실행되도록 하려면 <mark style="color:green;">`finally`</mark>절을 사용합니다. <mark style="color:green;">`catch`</mark>절이 예외를 잡은 경우 <mark style="color:green;">`catch`</mark>절 이후에 <mark style="color:green;">`finally`</mark>절이 수행되고, <mark style="color:green;">`catch`</mark>절이 예외를 잡지 못한 경우 <mark style="color:green;">`finally`</mark>절이 실행된 후 예외가 전파됩니다.

```dart
try {
  breedMoreLlamas();
} finally {
  // 예외가 발생하더라도 항상 정리 작업을 합니다.
  cleanLlamaStalls();
}

try {
  breedMoreLlamas();
} catch (e) {
  print('Error: $e'); // 예외를 먼저 처리한 후
} finally {
  cleanLlamaStalls(); // 정리 작업을 합니다.
}
```

