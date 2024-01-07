# 매개 변수

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

함수는 필요한 만큼의 **위치 매개변수(Positional parameters)**를 가질 수 있으며, 그 뒤에는 **명명된 매개변수(Named parameters)** 또는 **선택적 위치 매개변수(Optional positional parameters)**가 올 수 있습니다. [Flutter](https://flutter.dev/)의 위젯 생성자 같은 API의 경우 필수 매개변수의 경우에도 명명된 매개변수만 사용합니다.

함수에 인수를 전달하거나 함수 매개변수를 정의할 때 후행 쉼표를 사용할 수 있습니다. <mark style="color:red;">Dart</mark> 언어에서 기본으로 제공하는 [dart format](https://dart.dev/tools/dart-format) 커멘드라인 도구를 사용하면 후행 쉼표 유무에 따라 줄바꿈 처리가 다르게 적용됩니다.

### 명명된 매개변수 (Named parameters)

함수를 호출할 때 <mark style="color:green;">`paramName: value`</mark> 형태로 명명된 매개변수명을 지정할 수 있습니다. 명명된 매개변수는  <mark style="color:green;">`required`</mark>로 선언하지 않는한 선택적으로 사용할 수 있습니다. 함수를 정의할 때 <mark style="color:green;">`{param1, param2, …}`</mark>의 형태로 명명된 매개변수를 정의합니다.

```dart
void enableFlags({bool? bold, bool? hidden}) {
  ...
}

enableFlags(bold: true, hidden: false);
```

명명된 매개변수는 일종의 선택적 매개변수이지만 <mark style="color:green;">`required`</mark>로 선언하여 필수 매개변수 임을 나타낼 수 있습니다. 사용자는 반드시 매개변수의 값을 제공해야하며, 그렇지 않을 시 컴파일러는 오류를 발생시킵니다.

```dart
const Scrollbar({Key? key, required Widget child})
```

### 선택적 위치 매개변수 (Optional positional parameters)

함수 선언 시 매개변수를 <mark style="color:green;">`[]`</mark>로 감싸면 선택적 위치 매개변수로 정의됩니다. 예제에서 세번째 파라미터는 <mark style="color:green;">`device`</mark>를 사용할지는 사용자의 몫입니다.

```dart
void main() {
  print(say('Bob', 'Howdy'));
  print(say('Bob', 'Howdy', 'smoke signal'));
}

String say(String from, String msg, [String? device]) {
  var result = '$from says $msg';
  if (device != null) {
    result = '$result with a $device';
  }
  return result;
}
```

{% embed url="https://dartpad.dev/?id=dd9d376879ccadcf4884e2e718f5a2dd" %}

### 기본 매개변수 값 (Default parameter values)

함수는 <mark style="color:green;">`=`</mark>를 사용하여 명명된 매개변수와 선택적 위치 매개변수 모두에 대한 선택적 매개변수의 기본값을 정의할 수 있습니다. 기본값은 반드시 컴파일 타임 상수여야 합니다. 기본값이 제공되지 않을 경우 기본값은 <mark style="color:green;">`null`</mark>입니다. 다음은 명명된 매개변수의 기본값을 설정하는 예제입니다.

```dart
void enableFlags({bool bold = false, bool hidden = false}) {
  ...
}

enableFlags(bold: true);
```

이제 선택적 매개변수에 값을 넘기지 않았을 경우 기본값을 사용하도록 처리할 수 있습니다. 뿐만아니라 **Non-Nullable 타입**을 사용할 수 있게되어 번거로운 <mark style="color:green;">`null`</mark> 검사를 피할 수 있게 되었습니다. 선택적 위치 매개변수에 기본값을 설정하는 예제입니다.

```dart
void main() {
  print(say('Bob', 'Howdy'));
}

String say(String from, String msg, [String device = 'carrier pigeon']) {
  var result = '$from says $msg with a $device';
  return result;
}
```

{% embed url="https://dartpad.dev/?id=f5610435d0b85ff207920edb79ee4c30" %}

기본값으로 리스트나 맵 리터럴을 전달하는 것도 가능합니다.

```dart
void main() {
  doStuff();
}

void doStuff(
    {List<int> list = const [1, 2, 3],
    Map<String, String> gifts = const {
      'first': 'paper',
      'second': 'cotton',
      'third': 'leather'
    }}) {
  print('list:  $list');
  print('gifts: $gifts');
}
```

{% embed url="https://dartpad.dev/?id=79aa1b4a43bf5c710214a298da0362cb" %}
