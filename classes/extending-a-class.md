# 상속

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:green;">`extends`</mark> 키워드를 이용해 서브 클래스를 생성하며, <mark style="color:green;">`super`</mark> 키워드를 이용해 슈퍼 클래스를 참조합니다.

```dart
class Television {
  void turnOn() {
    _illuminateDisplay();
    _activateIrSensor();
  }
  
  // ···
}

class SmartTelevision extends Television {
  void turnOn() {
    super.turnOn();
    _bootNetworkInterface();
    _initializeMemory();
    _upgradeApps();
  }
  
  // ···
}
```

#### 멤버 재정의

서브 클래스는 인스턴스 메서드, 연산자 메서드, **getter**, **setter**를 재정의 할 수 있습니다. @override 에너테이션을 이용해 의도적으로 재정의하고 있음을 나타낼 수 있습니다.

```dart
class Television {
  // ···
  set contrast(int value) {...}
}

class SmartTelevision extends Television {
  @override
  set contrast(num value) {...}
  // ···
}
```

재정의하는 메서드는 아래의 일반 규칙을 만족해야 합니다.

* 반환 타입은 재정의된 반환 타입과 동일하거나 서브 타입이어야 합니다.
* 인수의 타입은 재정의된 메서드의 인수 타입과 동일하거나 슈퍼 타입이어야 합니다. 위 코드에서 <mark style="color:green;">`contrast`</mark>의 인수 <mark style="color:green;">`value`</mark>의 타입은 <mark style="color:green;">int</mark>에서 상위 타입인 <mark style="color:green;">`num`</mark>으로 변경했습니다.
* 재정의된 메서드가 n개의 위치 매개변수를 갖고 있다면, 재정의하는 메서드도 n개의 위치 매개변수를 가져야합니다.
* [제네릭 메서드](https://dart.dev/guides/language/language-tour#using-generic-methods)는 제네릭이 아닌 메서드를 재정의할 수 없고, 제네릭이 아닌 메서드는 제네릭 메서드를 재정의할 수 없습니다.

때로는 메서드 인수 또는 인스턴스 변수의 타입을 좁히고 싶을 수 있습니다. 이는 일반 규칙을 위반하며 런타임 시 유형 오류를 일으킬 수 있습니다. 그러나 이런 오류를 발생하지 않도록 보장할 수 있는 경우 [covariant](https://dart.dev/guides/language/sound-problems#the-covariant-keyword) 키워드를 이용해 타입을 좁힐 수 있습니다.

{% hint style="info" %}
만약 <mark style="color:green;">`==`</mark> 연산자 메서드를 재정의하는 경우 <mark style="color:green;">`Object`</mark> 클래스의 <mark style="color:green;">`hashCode`</mark> **getter**도 재정의 해야합니다.
{% endhint %}
