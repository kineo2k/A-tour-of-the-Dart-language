---
description: Important concepts
---

# Dart 언어의 중요한 개념들

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

아래와 같은 사실과 개념을 바탕으로 <mark style="color:red;">Dart</mark> 언어를 공부해주세요.



### 모든 것은 객체입니다.

변수에 할당 가능한 모든 것은 객체이고 모든 객체는 클래스의 인스턴스입니다. 숫자, 함수 및 <mark style="color:green;">`null`</mark> 조차도 객체입니다. [null safety](https://dart.dev/null-safety)(<mark style="color:red;">Dart</mark> 버전 2.12부터 지원)를 활성화한 상태의 <mark style="color:green;">`null`</mark>을 제외하고 모든 객체는 <mark style="color:green;">`Object`</mark> 클래스를 상속합니다. null safety를 사용할때 <mark style="color:green;">`null`</mark>은 <mark style="color:green;">`Null`</mark> 클래스를 상속하며, <mark style="color:green;">`Null`</mark> 클래스는 <mark style="color:green;">`Object`</mark> 클래스를 상속하지 않는 유일한 클래스입니다. <mark style="color:green;">`Null`</mark> 클래스를 상속하려고 시도하면 경우 컴파일 타임에 오류가 발생합니다. 보다 자세한 설명은 [여기](https://api.dart.dev/stable/2.16.0/dart-core/Null-class.html)를 참고해주세요.

![](.gitbook/assets/hierarchy-after.png)

```dart
void main() {
  // 변수에 할당 가능한 모든 것은 객체이며, Object 클래스를 상속합니다.
  print("int is Object: ${1 is Object}");
  print("double is Object: ${1.0 is Object}");
  print("bool is Object: ${true is Object}");
  print("String is Object: ${"Gump" is Object}");
  print("List is Object: ${[] is Object}");
  print("Function is Object: ${(){} is Object}");

  // Dart 2.12에서 도입된 null safety를 사용하면, null만 예외적으로 Null 클래스를 상속합니다.
  print("null is Object: ${null is Object}");
  print("null is Null: ${null is Null}");

  // Null 클래스는 인스턴스화할 수 없으며, null 예약어는 Null 클래스의 유일한 인스턴스입니다.
  // print("Null is Null: ${Null() is Null}");
}
```

{% embed url="https://dartpad.dev/?id=3b97dfdcb62550b6e162d19d01fafa4b" %}

### 강타입 언어입니다.

<mark style="color:red;">Dart</mark>는 강타입(strongly typed) 언어입니다. 컴파일러는 타입을 추론하기 때문에 타입 선언을 할지는 선택 사항입니다.

```dart
void main() {
  // int 타입으로 추론
  var intValue = 1;

  // double 타입으로 추론
  var doubleValue = 1.0;

  // Object 타입으로 선언했지만 int 타입 객체를 가르킴
  Object objectValue = 1;

  // runtimeType은 Object 클래스의 속성으로 객체의 런타임 타입을 나타냅니다.
  print(intValue.runtimeType);
  print(doubleValue.runtimeType);
  print(objectValue.runtimeType);
}
```

{% embed url="https://dartpad.dev/?id=70a098cadf4232c63a7a8ba7658bb454" %}

### Null safety를 지원합니다.

[Null safety](https://dart.dev/null-safety)를 활성화하면 변수에 <mark style="color:green;">`null`</mark> 할당을 허용한다고 선언하지 않은 경우 <mark style="color:green;">`null`</mark>을 할당할 수 없습니다. <mark style="color:green;">`null`</mark> 할당을 허용(nullable)하도록 변수를 선언하려면 타입 선언에 <mark style="color:green;">`?`</mark>를 추가하면 됩니다. 변수를 사용하고자 할때 변수가 <mark style="color:green;">`null`</mark>이 아니라면 <mark style="color:green;">`!`</mark>를 사용해서 값을 사용할 수 있습니다.

```dart
void main() {
  int intValue = 1;
  // Nullable 변수가 아니므로 null을 할당할 수 없습니다.
  // intValue = null;
  
  // 타입 선언에 ?를 추가하여 nullable 변수로 선언하였고, 정수 또는 null 값을 가질 수 있습니다.
  int? nullableIntValue = 2;
  nullableIntValue = null;
  
  // nullableIntValue가 null을 가질 수 있으므로 적절한 null 처리가 되지 않으면 컴파일 오류가 발생합니다.
  // var sum = intValue + nullableIntValue;
  
  // 만약 nullableIntValue가 null이 아니라고 확실한 수 있다면 !를 추가하여 컴파일러에게 null이 아님을 알려줍니다.
  var sum = intValue + nullableIntValue!;
  
  // nullableIntValue는 null이므로 위 연산은 런타임 오류가 발생합니다.
  // Uncaught TypeError: Cannot read properties of null (reading 'toString')Error: TypeError: Cannot read properties of null (reading 'toString')
}
```

{% embed url="https://dartpad.dev/?id=24996280a41f9820ccc62a6cfae50897" %}

### Object 또는 dynamic을 이용해 모든 타입을 수용 수 있습니다.

명시적으로 어떤 타입이든 허용하고 싶다면 <mark style="color:green;">`Object?, Object, dynamic`</mark>을 사용할 수 있습니다. 특히 dynamic은 REST API 이용한 데이터 불러오기 처럼 반드시 런타임(Runtime)에 타입 체킹을 해야하는 상황에서 유용하게 사용할 수 있습니다. 하지만, 컴파일 타임 타입 검사를 통한 장점이 사라지므로 반드시 필요한 경우에만 사용하는 것을 추천합니다.

### 제네릭을 지원합니다.

제네릭(Generic) 타입을 지원합니다. <mark style="color:green;">`List<int>`</mark>는 정수 리스트를 표현합니다.

### 다양한 함수 사용을 지원합니다.

* <mark style="color:green;">`main()`</mark> 함수와 같은 최상위 레벨 함수
* 클래스에 연결된 <mark style="color:green;">`static`</mark> 메서드
* 객체에 연결된 인스턴스 메서드
* 함수 안에서 함수를 정의하고 반환할 수 있음

### 다양한 변수 사용을 지원합니다.

* 최상위 레벨 변수
* 클래스에 연결된 <mark style="color:green;">`static`</mark> 변수
* 객체에 연결된 인스턴스 변수

### 식별자 명명 규칙이 존재합니다.

변수 및 함수 식별자(Identifiers)는 문자 또는 밑줄(<mark style="color:green;">`_`</mark>)로 시작해야 합니다. 이어서 문자와 숫자 조합을 사용할 수 있습니다.

### 접근 제한자를 지원하지 않습니다.

다른 언어에서 지원하는 <mark style="color:green;">`public, protected, private`</mark> 같은 접근 제한자를 지원하지 않습니다. 대신에 변수 또는 함수 식별자가 밑줄(<mark style="color:green;">`_`</mark>)로 시작하면 해당 라이브러리에 대해 비공개로 설정됩니다. 보다 자세한 내용은 [여기](https://dart.dev/guides/language/language-tour#libraries-and-visibility)를 참고해주세요.

### 표현식과 명령문을 모두 가지고 있습니다.

런타임에 값을 갖는 표현식(Expressions)과 값을 갖지 않는 명령문(Statements)을 모두 가지고 있습니다. 예로, 삼항 연산자 (<mark style="color:green;">`condition ? expr1 : expr2`</mark>)와 <mark style="color:green;">`if-else`</mark>문을 들 수 있습니다. <mark style="color:green;">`expr1, expr2`</mark>가 값이므로 삼항 연산자의 결과도 값인데 반해, if-else 문은 값을 갖지 않습니다. 명령문은 표현식을 포함할 수 있지만, 표현식은 명령문을 포함할 수 없습니다.

### Dart의 도구는 경고와 오류라는 두 종류의 문제를 보고합니다.

경고(Warnings)는 코드가 정상적으로 동작하지 않을 수 있다는 표현일 뿐 프로그램이 동작하는 것을 막지 않습니다. 오류(Errors)는 컴파일 타임과 런타임 오류가 있습니다. 컴파일 타임 오류는 프로그램이 실행될 수 없도록 막습니다. 런타임 오류는 프로그램이 실행되는 도중에 예외(Exception)를 발생 시킵니다.
