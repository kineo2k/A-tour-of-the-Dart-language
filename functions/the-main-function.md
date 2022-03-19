# main() 함수

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

모든 앱에는 앱의 **진입점(Entrypoint)** 역할을 하는 최상위 함수 <mark style="color:green;">`main()`</mark>이 있어야 합니다. <mark style="color:green;">`main()`</mark> 함수는 리턴 타입이 <mark style="color:green;">`void`</mark>이고 <mark style="color:green;">`List<String>`</mark> 타입의 선택적 매개변를 갖습니다. 다음은 간단한 <mark style="color:green;">`main()`</mark> 함수입니다.

```dart
void main() {
  print('Hello, World!');
}
```

**커멘드 라인(Command line)** 앱으로부터 인수를 받아서 사용하는 예제입니다.

```dart
void main(List<String> arguments) {
  print(arguments);
  print(arguments.length);
  print(arguments[0]);
  print(arguments[1]);
  print(arguments[2]);
}

<결과출력>
> dart args.dart Gump Edgar Bob
3
Gump
Edgar
Bob
```

{% embed url="https://dartpad.dev/?id=413a517d1d5bb1afce2d9c91f64cb62f" %}

[args library](https://pub.dev/packages/args) 패키지를  사용하면 커멘드 라인 인자를 정의하고 파싱할 수 있습니다.
