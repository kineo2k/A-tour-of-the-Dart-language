# 문자열

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:red;">Dart</mark>의 문자열은 <mark style="color:green;">`String`</mark> 타입으로 제공되며, 일련의 UTF-16 코드 단위를 갖습니다. [UTF-16을 사용하는 이유](https://github.com/dart-lang/sdk/issues/36316)가 궁금해서 찾아봤습니다.

<mark style="color:red;">Dart</mark>는 브라우저에서 사용할 수 있도록 설계되으며, <mark style="color:red;">dart2js</mark> 컴파일러를 이용해서 <mark style="color:red;">JavaScript</mark>로 컴파일합니다. 만약 <mark style="color:red;">Dart</mark>의 문자열이 <mark style="color:red;">JavaScript</mark>와 많이 다르다면 컴파일 시 문자열 관련 작업이 비효율적이었을 것입니다. 이런 이유로 <mark style="color:red;">Dart</mark> 문자열은 [JavaScript의 문자열과 동일한 UTF-16](https://stackoverflow.com/questions/11141136/what-is-the-default-javascript-character-encoding)으로 설계되었습니다.

문자열은 작은 따옴표나 큰 따옴표를 사용하여 만들 수 있습니다. <mark style="color:green;">`${표현식}`</mark>을 이용하여 문자열에 값으로 평가되는 표현식을 넣을 수(String interpolation) 있습니다. 표현식이 식별자인 경우 <mark style="color:green;">`{}`</mark>을 생략할 수 있습니다. 표현식의 평가 결과가 객체인 경우 객체의 <mark style="color:green;">`toString()`</mark> 메서드를 호출합니다.

```dart
void main() {
  var s1 = 'Single quotes work well for string literals.';
  var s2 = "Double quotes work just as well.";
  var s3 = 'It\'s easy to escape the string delimiter.';
  var s4 = "It's even easier to use the other delimiter.";
  
  var s = 'string interpolation';

  assert('Dart has $s, which is very handy.' ==
    'Dart has string interpolation, '
        'which is very handy.');
  assert('That deserves all caps. '
        '${s.toUpperCase()} is very handy!' ==
    'That deserves all caps. '
        'STRING INTERPOLATION is very handy!');
}
```

{% embed url="https://dartpad.dev/?id=37f71da0f9f714b54753346b24502339" %}

<mark style="color:green;">`+`</mark> 연산자는 인접한 두 문자열을 연결할 수 있습니다. <mark style="color:green;">`==`</mark> 연산자는 인접한 두 문자열을 비교하여 동일한 문자열 값을 갖는지 평가합니다.

```dart
void main() {
  var s1 = 'String '
    'concatenation'
    " works even over line breaks.";
  assert(s1 ==
    'String concatenation works even over '
        'line breaks.');

  var s2 = 'The + operator ' + 'works, as well.';
  assert(s2 == 'The + operator works, as well.');
}
```

{% embed url="https://dartpad.dev/?id=5e79dbd1b35e6ea5db4453230cbcdd58" %}

삼중 따옴표(<mark style="color:green;">`'''`</mark>)를 이용해 다중 라인 문자열을 만들 수 있습니다. 또한 문열 표현식 앞에 <mark style="color:green;">`r`</mark>을 붙여서 원시 문자열을 만들 수 있습니다.

```dart
void main() {
  var s1 = '''
You can create
multi-line strings like this one.
''';
  print(s1);
  
  var s2 = """This is also a
multi-line string.\n""";
  print(s2);
  
  var s3 = r'In a raw string, not even \n gets special treatment.';
  print(s3);
}

<출력결과>
You can create
multi-line strings like this one.

This is also a
multi-line string.

In a raw string, not even \n gets special treatment.
```

{% embed url="https://dartpad.dev/?id=afa334c08425808d29c1839744e83b98" %}

문자열 리터럴은 컴파임 타임 상수입니다. 또한 <mark style="color:green;">`null`</mark>, 상수 숫자, 문자열, 부울 값으로 구성된 String interpolation도 컴파일 타임 상수입니다.

```dart
void main() {
  // 컴파일 타임 상수를 정의합니다.
  const aConstNum = 0;
  const aConstBool = true;
  const aConstString = 'a constant string';

  // 아래 정의한 변수나 상수 리스트는 String interpolation에서 사용할 수 없습니다.
  var aNum = 0;
  var aBool = true;
  var aString = 'a string';
  const aConstList = [1, 2, 3];

  const validConstString = '$aConstNum $aConstBool $aConstString ';
  // const invalidConstString = '$aNum $aBool $aString $aConstList';
}
```

{% embed url="https://dartpad.dev/?id=7f775dd2ddd378f95fac73d4d5fa122d" %}
