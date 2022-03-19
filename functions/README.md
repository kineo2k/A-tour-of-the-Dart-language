# 함수

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:red;">Dart</mark> 언어는 순수 객체 지향 언어로 함수도 객체이며, [Function](https://api.dart.dev/stable/2.16.1/dart-core/Function-class.html) 타입을 갖습니다. 이 말은 함수를 변수에 할당하고 다른 함수의 인자로 전달할 수 있습니다. 또한, 클래스 인스턴스를 함수 처럼 호출(Callable classes)할 수도 있습니다. 보다 자세한 내용은 [여기](https://dart.dev/guides/language/language-tour#callable-classes)를 참고해주세요.

다음은 함수를 구현하는 예제입니다. 재있는 사실은 함수 선언 시 인자나 반환값 타입을 생략해도 잘 동작한다는 것입니다. 하지만 [추천되는 방법](https://dart.dev/guides/language/effective-dart/design#do-type-annotate-fields-and-top-level-variables-if-the-type-isnt-obvious)은 아니므로 반드시 타입을 함께 사용해주세요.

```dart
void main() {
  print("Sum with type : ${sumWithType(2, 3)}");
  print("Sum without type : ${sumWithType(2, 3)}");
  print("Sum without type : ${sumWithoutType("Hello", "World")}");
}

int sumWithType(int a, int b) {
  return a + b;
}

sumWithoutType(a, b) {
  return a + b;
}
```

{% embed url="https://dartpad.dev/?id=fb01b561c186e5caafb174ed86472efd" %}

함수의 바디에 하나의 표현식(Expression)만 존재할 경우 **화살표 구문**(<mark style="color:green;">`=>`</mark>)이라 불리는 단축 구문을 사용할 수 있습니다. 화살표 구문은 <mark style="color:green;">`{}`</mark>와 <mark style="color:green;">`return`</mark>을 생략할 수 있습니다.

```dart
int sumWithType(int a, int b) => a + b;
```

함수의 반환값 타입으로  <mark style="color:green;">`void`</mark>를 지정하지 않으면 모든 함수는 값을 반환합니다. 만약 반환 값을 명시하지 않는다면 암시적으로 <mark style="color:green;">`return null;`</mark>이 함수 끝에 추가됩니다.

```
void main() {
  print(foo()); // null
}

foo() {}
```
