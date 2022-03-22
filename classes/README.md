# 클래스

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

<mark style="color:red;">Dart</mark>는 **클래스(Class)**와 **믹스인(Mixin)** 기반의 상속을 지원하는 **객체 지향 언어**입니다. 모든 객체는 클래스의 인스턴스이며, <mark style="color:green;">`Null`</mark>의 유일한 객체인 <mark style="color:green;">`null`</mark>을 제외하고 객체는 [Object](https://api.dart.dev/stable/2.16.1/dart-core/Object-class.html) 클래스를 상속합니다. 믹스인 기반의 상속은 모든 클래스가 하나의 부모 클래스만 갖지만, 클래스 바디는 여러 클래스 계층으로부터 재사용 할 수 있음을 이야기합니다. **확장 메서드(Extentions methods)**는 클래스를 변경하거나 하위 클래스를 만들지 않고 클래스에 기능을 추가하는 방법입니다.
