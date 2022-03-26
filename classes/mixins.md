# 믹스인

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

**믹스인(Mixin)**은 여러 클래스 계층에서 클래스 코드를 재사용하는 방법입니다. 믹스인을 사용하려면 <mark style="color:green;">`with`</mark> 키워드 다음에 믹스인 이름을 나열합니다. 아래 코드는 믹스인을 사용하는 예제입니다.

```dart
class Musician extends Performer with Musical {
  // ···
}

class Maestro extends Person with Musical, Aggressive, Demented {
  Maestro(String maestroName) {
    name = maestroName;
    canConduct = true;
  }
}
```

믹스인을 구현하려면 <mark style="color:green;">`Object`</mark>를 확장하고 생성자를 선언하지 않는 클래스를 만듭니다. 믹스인을 일반 클래스로 사용하지 않으려면 <mark style="color:green;">`class`</mark> 대신 <mark style="color:green;">`mixin`</mark> 키워드를 사용하세요.

```dart
mixin Musical {
  bool canPlayPiano = false;
  bool canCompose = false;
  bool canConduct = false;

  void entertainMe() {
    if (canPlayPiano) {
      print('Playing piano');
    } else if (canConduct) {
      print('Waving hands');
    } else {
      print('Humming to self');
    }
  }
}
```

때때로 <mark style="color:green;">`mixin`</mark>을 사용할 수 있는 타입을 제한하고 싶을 수 있습니다. 이런 경우 <mark style="color:green;">`on`</mark> 키워드를 이용해 필요한 슈퍼 클래스를 지정하여 <mark style="color:green;">`mixin`</mark>의 사용을 제한할 수 있습니다.

```dart
class Musician {
  // ...
}

// Musician의 하위 타입만 MusicalPerformer 믹스인을 사용할 수 있습니다.
mixin MusicalPerformer on Musician {
  // ...
}

// SingerDancer는 Musician의 서브 클래스이므로 MusicalPerformer 믹스인을 사용할 수 있습니다.
class SingerDancer extends Musician with MusicalPerformer {
  // ...
}
```

슈퍼 클래스 및 믹스인에서 동형의 메서드를 제공하고 있을 경우 마지막에 선언된 믹스인의 구현이 사용됩니다.

```dart
class SuperA {
  void printMe() {
    print("SuperA");
  }
}
mixin MixinA {
  void printMe() {
    print("MixinA");
  }
}

mixin MixinB {
  void printMe() {
    print("MixinB");
  }
}

class Test extends SuperA with MixinA, MixinB {
}

void main() {
  Test().printMe();
}

<출력결과>
MixinB
```

{% embed url="https://dartpad.dev/?id=6cba87a5a95566f09a3d07799a320f1c" %}
