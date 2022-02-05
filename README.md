# Dart 언어 둘러보기

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

![](.gitbook/assets/Dart.png)

## 기본적인 다트 프로그

```dart
// 함수를 정의합니다.
void printInteger(int aNumber) {
  print('The number is $aNumber.');  // 콘솔에 출력합니다.
}

// Dart 프로그램은 main 함수에서 시작합니다. (Entry point)
void main() {
  var number = 42; // 변수를 선언하고 초기화 합니다.
  printInteger(number); // 함수를 호출합니다.
}
```

{% embed url="https://dartpad.dev/71448afab00f1b4ded8a50e3fdaa397c" %}

이 예제는 Dart 프로그램에 대해 많은 것을 알려줍니다.
