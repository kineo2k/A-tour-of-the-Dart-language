# Dart 언어 둘러보기

> [A tour of the Dart language](https://dart.dev/guides/language/language-tour) 페이지를 공부하면서 정리한 내용입니다.

![](.gitbook/assets/Dart.png)

## 기본적인 다트 프로그

```dart
// Define a function.
void printInteger(int aNumber) {
  print('The number is $aNumber.'); // Print to console.
}

// This is where the app starts executing.
void main() {
  var number = 42; // Declare and initialize a variable.
  printInteger(number); // Call a function.
}
```

{% embed url="https://dartpad.dev/71448afab00f1b4ded8a50e3fdaa397c" %}
