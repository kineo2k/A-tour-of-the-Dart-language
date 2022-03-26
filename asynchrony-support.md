# 비동기 지원

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

Dart 라이브러리는 [Future](https://api.dart.dev/stable/2.16.2/dart-async/Future-class.html) 또는 [Stream](https://api.dart.dev/stable/2.16.2/dart-async/Stream-class.html) 객체를 반환하는 함수로 가득합니다. 이런 함수는 **비동기식(Asynchronous)**으로 동작하는데 I/O 같이 시간이 많이 소요될 수 있는 작업을 실행하고 해당 작업이 완료될 때까지 기다리지 않고 즉시 반환됩니다.

<mark style="color:green;">`async`</mark> 및 <mark style="color:green;">`await`</mark> 키워는 비동기 프로그래밍 코드를 동기 프로그래밍 코드와 유사하게 작성할 수 있도록 지원합니다.

#### Future 다루기

작업이 완료된 <mark style="color:green;">`Future`</mark>의 결과가 필요한 경우 두 가지 옵션이 있습니다.

* [async 및 await](https://dart.dev/codelabs/async-await)를 사용해서 결과를 처리하기
* [Future API](https://dart.dev/guides/libraries/library-tour#future)를 사용해서 결과를 처리하기

<mark style="color:green;">`async`</mark> 및 <mark style="color:green;">`await`</mark>를 사용하는 코드는 비동기식이지만 동기식 코드와 유사합니다. 아래 코드는 <mark style="color:green;">`await`</mark>를 사용하여 비동기 함수의 결과를 기다리는 코드입니다.

```dart
final version = await lookUpVersion();
```

<mark style="color:green;">`await`</mark>를 사용하려면 반드시 함수 선언이 <mark style="color:green;">`async`</mark>로 되어야 합니다.

```dart
Future<void> checkVersion() async {
  // lookUpVersion() 함수는 비동기 함수지만,
  // lookUpVersion() 처리가 완료될때까지 대기했다가 다음 행의 코드가 수행됩니다.
  var version = await lookUpVersion();
  
  // version을 알았으므로 version을 처리합니다.
}
```

<mark style="color:green;">`await`</mark>를 사용할 경우 동기식 코드와 동일한 방법으로 예외 처리합니다.

```dart
try {
  version = await lookUpVersion();
} catch (e) {
  // 버전 조회에 실패한 경우 예외 처리를 합니다.
}
```

<mark style="color:green;">`async`</mark> 함수에서 <mark style="color:green;">`await`</mark>를 여러번 사용할 수 있습니다.

```dart
var entrypoint = await findEntryPoint();
var exitCode = await runExecutable(entrypoint, args);
await flushThenExit(exitCode);
```

<mark style="color:green;">`await`</mark> 표현식에서 표현식의 값은 <mark style="color:green;">`Future`</mark>입니다. 만약 <mark style="color:green;">`Futrue`</mark> 타입이 아닌 경우 자동으로 <mark style="color:green;">`Future`</mark>로 래핑(Wrapping)됩니다. <mark style="color:green;">`Future`</mark> 객체는 비동기 처리의 결과로 객체를 반환한다는 약속을 나타냅니다. <mark style="color:green;">`await`</mark> 표현식의 값은 반환된 객체입니다. <mark style="color:green;">`await`</mark> 표현식은 객체를 사용할 수 있을 때까지 실행을 일시 중지합니다.

<mark style="color:green;">`await`</mark>를 사용할때 컴파일 타임 에러가 발생한다면 해당 함수가 <mark style="color:green;">`async`</mark>로 선언되었는지 확인하세요. 예를 들어 <mark style="color:green;">`main()`</mark> 함수 바디에서 <mark style="color:green;">`await`</mark>를 사용한다면 <mark style="color:green;">`main()`</mark> 함수도 <mark style="color:green;">`async`</mark> 함수로 선언되어야 합니다.

```dart
void main() async {
  checkVersion();
  print('In main: version is ${await lookUpVersion()}');
}
```

#### 비동기 함수 선언하기

<mark style="color:green;">`async`</mark> 함수는 함수 바디 앞에 <mark style="color:green;">`async`</mark> 키워드를 붙여서 선언합니다. 함수에 <mark style="color:green;">`async`</mark>를 추가하면 <mark style="color:green;">`Future`</mark>를 반환합니다. String을 반환하는 동기식 함수를 예로 들어보겠습니다.

```dart
String lookUpVersion() => '1.0.0';
```

만약 버전을 확인하는데 시간이 오래 걸릴 것으로 예상한다면 <mark style="color:green;">`async`</mark> 함수로 선언합니다. 이 경우 반환 값은 <mark style="color:green;">`Futrue<String>`</mark>이 됩니다.

```dart
Future<String> lookUpVersion() async => '1.0.0';
```

함수의 바디에는 <mark style="color:green;">`Future`</mark> API를 사용할 필요가 없습니다. <mark style="color:red;">Dart</mark>는 필요한 경우에 자동으로 <mark style="color:green;">`Future`</mark> 객체를 생성해 반환합니다. 만약 함수가 값을 반환하지 않는다면 <mark style="color:green;">`Future<void>`</mark> 타입을 반환합니다.

```dart
import "dart:math";

class UnacceptableNumberException implements Exception {
  String cause;
  UnacceptableNumberException(this.cause);
}

Future<int> randomNumber() async {
  return Future.delayed(
    Duration(seconds: 1),
    () {
      final number = Random().nextInt(3);
      if (number == 0) {
        throw UnacceptableNumberException("0은 허용할 수 없습니다.");
      }

      return number;
    },
  );
}

void main() async {
  final rn1 = randomNumber();
  printTypeAndVlaue("Non-await", rn1);

  rn1.then((value) {
    printTypeAndVlaue("Non-await then", value);
  }).catchError((err) {
    printTypeAndVlaue("Non-await catch", err);
  });

  try {
    final rn2 = await randomNumber();
    printTypeAndVlaue("await", rn2);
  } on UnacceptableNumberException catch (err) {
    printTypeAndVlaue("await catch", err);
  }
}

void printTypeAndVlaue(String tag, dynamic obj) {
  print("$tag: Type=${obj.runtimeType}, Value=${obj}");
}
```

{% embed url="https://dartpad.dev/?id=c60248e884a1b4c96ff5034a9d034e2b" %}

#### Stream 다루기

<mark style="color:green;">`Stream`</mark>에서 값을 가져와야 하는 경우 두 가지 옵션이 있습니다.

* <mark style="color:green;">`async`</mark> 및 <mark style="color:green;">`await for`</mark> 사용해서 결과를 처리하기
* [Stream API](https://dart.dev/guides/libraries/library-tour#stream)를 사용해서 결과를 처리하기

await for는 다음과 같이 사용합니다.

```dart
await for (varOrType identifier in expression) {
  // Stream이 값을 내보낼 때마다 수행됩니다.
}
```

<mark style="color:green;">`expression`</mark>의 값은 <mark style="color:green;">`Stream`</mark> 타입이어야 합니다. 다음 순서로 실행됩니다.

1. <mark style="color:green;">`Stream`</mark>이 값을 내놓을 때까지 대기합니다.
2. 변수가 값으로 설정된 상태에서 <mark style="color:green;">`for`</mark> 루프의 바디가 실행됩니다.
3. <mark style="color:green;">`Stream`</mark>이 닫힐 때까지 1, 2를 반복합니다.

<mark style="color:green;">`Stream`</mark>에서 값 수신을 중지하려면 <mark style="color:green;">`break`</mark>나 <mark style="color:green;">`return`</mark> 문을 사용합니다.

```dart
import "dart:math";

Stream<int> randomStream() {
  final rng = Random();
  return Stream<int>.periodic(
      const Duration(seconds: 1), (x) => rng.nextInt(7) + 1);
}

void main() async {
  await for (final randomNumber in randomStream()) {
    print("Current number: $randomNumber");
    
    if (randomNumber == 7) {
      print("Lucky 7");
      break;
    }
  }
}
```

{% embed url="https://dartpad.dev/?id=ae3fee914056722d1b0238ab622bf5df" %}
