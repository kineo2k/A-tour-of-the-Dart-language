# Map

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

**맵**은 **키(Key)**와 **값(Value)**을 연결하는 객체입니다. **키**와 **값**은 어떤 타입의 객체든 사용할 수 있습니다. **키**는 고유한 값으로 중복을 허용하지 않지만, **값**은 동일한 값이 중복으로 사용되는 것을 허용합니다. <mark style="color:red;">Dart</mark>에서는 <mark style="color:green;">`Map`</mark> 타입을 통해 **맵**을 지원하며 리터럴 표현식도 지원합니다.

```dart
void main() {
  // Map 리터럴 표현식으로 Map<String, String>으로 타입 추론됩니다.
  var gifts = {
    // 키: 값
    'first': 'partridge',
    'second': 'turtledoves',
    'fifth': 'golden rings'
  };

  // Map<int, String>으로 타입 추론됩니다.
  var nobleGases = {
    2: 'helium',
    10: 'neon',
    18: 'argon',
  };

  // Map 생성자를 이용해서 맵 객체를 생성합니다.
  var gifts = Map<String, String>();
  gifts['first'] = 'partridge';
  gifts['second'] = 'turtledoves';
  gifts['fifth'] = 'golden rings';

  var nobleGases = Map<int, String>();
  nobleGases[2] = 'helium';
  nobleGases[10] = 'neon';
  nobleGases[18] = 'argon';
}

```

{% embed url="https://dartpad.dev/?id=75f9227c954fd125cc329ceeb0d6864a" %}

**맵**에 **키**와 **값**을 추가할때는 <mark style="color:green;">`맵객체[키] = 값`</mark>을 사용합니다. <mark style="color:green;">`맵객체[키]`</mark>를 사용하여 **값**을 조회할 수 있습니다. **맵**에 조회 시 **키**가 존재하지 않을 경우 <mark style="color:green;">`null`</mark>을 반환합니다. <mark style="color:green;">`length`</mark> 속성을 이용하여 **맵**의 항목 수를 조회할 수 있습니다.

```dart
void main() {
  var gifts = {'first': 'partridge'};

  // 키와 값을 추가합니다.
  gifts['fourth'] = 'calling birds';

  // 키로 값을 조회할 수 있습니다.
  assert(gifts['first'] == 'partridge');

  // Map에 키가 존재하지 않으면 null을 반환합니다.
  assert(gifts['fifth'] == null);

  // Map의 항목수를 조회합니다.
  assert(gifts.length == 2);
}
```

{% embed url="https://dartpad.dev/?id=d40b3385199b92ea0e0602dd0c503e73" %}

<mark style="color:green;">`Map`</mark> 리터럴 앞에 <mark style="color:green;">`const`</mark> 키워드를 붙이면 컴파일 타임 상수로 선언할 수 있습니다. <mark style="color:green;">`Map`</mark> 타입도 <mark style="color:green;">`List`</mark> 타입과 같이 **전개 연산자**와 **collection if, for**를 사용할 수 있습니다.

```dart
void main() {
  final constantMap = const {
    2: 'helium',
    10: 'neon',
    18: 'argon',
  };

  // Uncaught Error: Unsupported operation: Cannot modify unmodifiable Map
  // constantMap[2] = 'Helium';

  Map<int, String> map = {for (int i = 0; i < 5; i++) i: "#$i"};
  print(map);
}
```

{% embed url="https://dartpad.dev/?id=681e8c17610418cce41e03a260353994" %}

<mark style="color:green;">`Map`</mark> 타입은 다양한 속성과 메서드를 제공하고 있습니다.

```dart
void main() {
  var map = {
    "KR": "KOREA",
    "US": "USA",
    "KP": "NORTH KOREA",
    "FR": "FRANCE",
    "FI": "FINLAND",
  };

  print("Map: $map");
  print("타입: ${map.runtimeType}, 항목수: ${map.length}");
  print("빈 Map 확인: ${map.isEmpty}, 아이템이 하나 이상 존재하는지 확인: ${map.isNotEmpty}");

  print("Map 줄단위 출력:");
  map.forEach((key, value) => print("{$key: $value}"));

  print("KR 키 존재 확인: ${map.containsKey("KR")}");
  print("KOREA 값 존재 확인: ${map.containsValue("KOREA")}");

  map.putIfAbsent("JP", () => "JAPAN");
  print("Map: $map");

  map.putIfAbsent("JP", () => "('-');");
  print("Map: $map");

  map.update("FR", (value) => "$value Kiss");
  print("Map: $map");

  map.remove("FI");
  print("Map: $map");

  map.removeWhere((key, value) => value.contains("KOREA"));
  print("Map: $map");

  map.clear();
  print("빈 Map 확인: ${map.isEmpty}, 아이템이 하나 이상 존재하는지 확인: ${map.isNotEmpty}");
}
```

{% embed url="https://dartpad.dev/?id=14f51ec581234ae671d0f7fa2b448876" %}
