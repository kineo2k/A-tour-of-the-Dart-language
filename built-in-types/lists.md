# List

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:red;">Dart</mark>에서는 배열은 <mark style="color:green;">`List`</mark> 타입으로 제공됩니다. 리스트 리터럴은 <mark style="color:red;">JavaScript</mark>의 배열과 유사항 방식으로 생성합니다. 아래 코드에서 <mark style="color:green;">`list`</mark>의 타입은 <mark style="color:green;">`List<int>`</mark> 타입으로 추론됩니다. <mark style="color:green;">`List<int>`</mark> 타입에 다른 타입을 추가하려고 시도하면 컴파잁 타임 또는 런타임 오류가 발생합니다. 보다 자세한 내용은 [여기](https://dart.dev/guides/language/type-system#type-inference)를 참고해주세요.

<mark style="color:red;">Dart</mark> 컬렉션 리터럴의 마지막 항목 뒤에 쉼표(<mark style="color:green;">`,`</mark>)를 추가할 수 있습니다. **후행 쉼표**(Trailing comma)는 컬렉션에 영향을 미치지 않지만, 복사-붙여넣기 시 오류를 방지할 수 있습니다. <mark style="color:green;">`List`</mark> 리터럴 앞에 <mark style="color:green;">`const`</mark> 키워드를 붙이면 컴파일 타임 상수로 선언할 수 있습니다.

```dart
void main() {
  // List<int> type
  var list1 = [1, 2, 3];
  
  list1.add(4);

  // Error: The argument type 'String' can't be assigned to the parameter type 'int'.
  // list1.add("String");

  var list2 = [
    'Car',
    'Boat',
    'Plane', // 리스트 요소 끝내 콤마를 추가할 수 있습니다.
  ];
  
  var constantList = const [1, 2, 3];
  // Error: Unsupported operation: indexed set
  // constantList[1] = 1;
}
```

{% embed url="https://dartpad.dev/?id=c224f6b6dbacd77b1517243856860f03" %}

<mark style="color:green;">`List`</mark> 객체의 인덱스는 <mark style="color:green;">`0`</mark>부터 시작하고 <mark style="color:green;">`list.length - 1`</mark>은 마지막 인덱스입니다. <mark style="color:green;">`length`</mark> 속성을 이용해 리스트의 길이를 알 수 있으며, 인덱스를 이용해 리스트 값을 참조할 수 있습니다.

```dart
void main() {
  var list = [1, 2, 3];
  assert(list.length == 3);
  assert(list[1] == 2);

  list[1] = 1;
  assert(list[1] == 1);
}
```

{% embed url="https://dartpad.dev/?id=38aa2eca9aa08983f6aeee23b3266241" %}

<mark style="color:red;">Dart</mark> 2.3부터 **전개 연산자**(Spread operator, <mark style="color:green;">`...`</mark>)와 **Null-aware 전개 연산자**(<mark style="color:green;">`...?`</mark>)를 도입하여 여러 값을 컬렉션에 삽입하는 편리한 방법을 제공하기 시작했습니다. 보다 자세한 내용은 [여기](https://github.com/dart-lang/language/blob/master/accepted/2.3/spread-collections/feature-specification.md)를 참고해주세요.

```dart
void main() {
  // list2에 list의 각 항목을 추가합니다.
  var list = [1, 2, 3];
  var list2 = [0, ...list];
  assert(list2.length == 4);

  List<int>? list3 = nullableList();
  
  // list3이 null이 아닌 경우에만 list3의 항목을 전개합니다.
  var list4 = [0, ...?list3];
  assert(list4.length == 1);
}

List<int>? nullableList() => null;
```

{% embed url="https://dartpad.dev/?id=5fe347ad77d948c793ce5c90277225a7" %}

<mark style="color:red;">Dart</mark>는 조건부와 반복을 사용하여 컬렉션을 생성할 수 있도록 해주는 **collection if**와 **collection for**를 제공합니다.

* **collection if** : 조건식을 평가하여 true인 경우 표현식을 평가하여 컬렉션에 항목을 추가합니다.
* **collection for** : 루프를 순회하며 표현식을 평하여 컬렉션에 항목을 추가합니다.

**collection if와 for**에 대한 자세한 내용은 [여기](https://github.com/dart-lang/language/blob/master/accepted/2.3/control-flow-collections/feature-specification.md)를 참고해주세요. [제네릭](https://dart.dev/guides/language/language-tour#generics)과 [컬렉션](https://dart.dev/guides/libraries/library-tour#collections)에 대한 자세한 내용은 링를 참고해주세요.

```dart
void main() {
  // promoActive가 true 일때 리스트에 'Outlet'을 추가합니다.
  bool promoActive = true;
  var nav = ['Home', 'Furniture', 'Plants', if (promoActive) 'Outlet'];
  print(nav);

  // listOfInts의 각 요소를 순회하면서 우측 표현식을 평가하여 리스트에 항목을 추가합니다.
  var listOfInts = [1, 2, 3];
  var listOfStrings = ['#0', for (var i in listOfInts) '#$i'];
  print(listOfStrings);
}

<출력결과>
[Home, Furniture, Plants, Outlet]
[#0, #1, #2, #3]
```

{% embed url="https://dartpad.dev/?id=fa44f2f0483ed8f6a38e41f517ee2d23" %}

<mark style="color:green;">`List`</mark> 타입은 다양한 속성과 메서드를 제공하고 있습니다.

```dart
void main() {
  var list = <String>["Gump", "Bob", "Edgar"];
  print("List: $list");
  print("타입: ${list.runtimeType}, 항목수: ${list.length}");
  print("첫번째 아이템: ${list.first}, 마지막 아이템: ${list.last}");
  print("빈 List 확인: ${list.isEmpty}, 아이템이 하나 이상 존재하는지 확인: ${list.isNotEmpty}");

  list.add("Owen");
  print("List: $list");

  list.addAll(["Binary", "Johnny"]);
  print("List: $list");
  print("List 줄단위 출력:");
  list.forEach(print);

  list.sort();
  print("List 정렬: $list");
  print("List 역순: ${list.reversed}");

  list.shuffle();
  print("List 셔플: $list");

  print("알파벳 B로 시작하는 이름 존재 확인: ${list.any((item) => item.startsWith("B"))}");
  print("알파벳 B로 시작하는 이름 찾기: ${list.where((item) => item.startsWith("B"))}");
  print("Bob 존재 확인: ${list.contains("Bob")}");
  print("Bob 인덱스 확인: ${list.indexOf("Bob")}");

  var dynamicList = <dynamic>[...list];
  print("String List로 변환: ${dynamicList.cast<String>()}");

  list.add("Gump");
  print("Map으로 변환: ${list.asMap()}");
  print("Set으로 변환: ${list.toSet()}");

  list.remove("Gump");
  print("List: $list");

  list.removeAt(1);
  print("List: $list");

  list.removeRange(1, 3);
  print("List: $list");

  list.clear();
  print("빈 List 확인: ${list.isEmpty}, 아이템이 하나 이상 존재하는지 확인: ${list.isNotEmpty}");
}
```

{% embed url="https://dartpad.dev/?id=82a24d111b9d128dfd0a06f41be37cb8" %}
