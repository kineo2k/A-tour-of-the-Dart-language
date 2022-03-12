# Set

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

**집합**은 정렬되지 않은 고유한 항목들로 이루어진 컬렉션입니다. <mark style="color:green;">`Set`</mark> 타입을 통해 제공되며 <mark style="color:green;">`{...}`</mark> 표현식으로 리터럴을 지원합니다.  아래 코드에서 <mark style="color:green;">`halogens`</mark> 변수는 <mark style="color:green;">`Set<String>`</mark> 타입으로 추론됩니다. <mark style="color:green;">`Set`</mark>에 다른 타입을 추가할 경우 컴파일 타임 또는 런타임 오류가 발생합니다. 타입 인수를 <mark style="color:green;">`{}`</mark>앞에 사용하거나 <mark style="color:green;">`Set`</mark> 변수에 할당하면 빈 <mark style="color:green;">`Set`</mark>을 생성합니다.

```dart
void main() {
  var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};

  // Error: The argument type 'int' can't be assigned to the parameter type 'String'.
  halogens.add(1);

  var names = <String>{};
  // 위와 동일한 표현식입니다.
  // Set<String> names = {};

  // 타입 어노테이션 없이 {}만 사용하면 Map 객체가 생성됩니다.
  var empty = {};
  print(empty.runtimeType);
}

```

{% embed url="https://dartpad.dev/?id=d152c2d66f7e90e2769fd0519bd38afb" %}

<mark style="color:green;">`Map`</mark> 리터럴 표현식은 <mark style="color:green;">`Set`</mark> 리터럴과 문법이 유사합니다. <mark style="color:green;">`Map`</mark> 리터럴이 더 먼저 지원되기 시작해서 <mark style="color:green;">`{}`</mark>의 기본 타은 <mark style="color:green;">`Map`</mark>입니다. <mark style="color:green;">`{}`</mark> 리터럴 사용 시 타입 어노테이션이 타입 인수를 선언하지 않으면 <mark style="color:green;">`Map<dynamic, dynamic>`</mark> 타입의 객체가 생성됩니다.

<mark style="color:green;">`Set`</mark>에 항목을 추가할 때는 <mark style="color:green;">`add()`</mark> 또는 <mark style="color:green;">`addAll()`</mark> 메서드 사용합니다. 또한 <mark style="color:green;">`length`</mark> 속성을 이용하여 항목의 수를 구합니다.

```dart
void main() {
  var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};
  var elements = <String>{};
  elements.add('fluorine');
  elements.addAll(halogens);
  assert(elements.length == 5);
}
```

{% embed url="https://dartpad.dev/?id=bf4b46ec86d9d5cbb824aba208bcbda9" %}

<mark style="color:green;">`Set`</mark> 리터럴 앞에 <mark style="color:green;">`const`</mark> 키워드를 붙이면 컴파일 타임 상수로 선언할 수 있습니다. <mark style="color:green;">`Set`</mark> 타입도 <mark style="color:green;">`List`</mark> 타입과 같이 **전개 연산자**와 **collection if, for**를 사용할 수 있습니다.

```dart
void main() {
  final constantSet = const {
    'fluorine',
    'chlorine',
    'bromine',
    'iodine',
  };

  // Unsupported operation: Cannot change an unmodifiable set
  constantSet.add("astatine");

  Set<int> set = {for (int i = 0; i < 5; i++) i};
  print(set);
}

```

{% embed url="https://dartpad.dev/?id=a4b7b52c2c5e9b4c8f44612833094659" %}
