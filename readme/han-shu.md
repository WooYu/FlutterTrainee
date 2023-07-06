# 函数

## 命名参数和默认参数

* 外部调用能够明确入参含义
* 无需按照参数顺序传递

```dart
main() {
  solution(foot: 194);
  solution(
    foot: 194,
    head: 85,
  );
}

void solution({
  int head = 88,
  required int foot,
}) {
  print("头数:$head  足数:$foot");
  int y = (foot - head * 2) ~/ 2;
  int x = head - y;
  print("雉数:$x  兔数:$y");
}
```



## 可选参数

* 可选参数，必须按照顺序传递

```dart
  DateTime(int year,
        [int month = 1,
        int day = 1,
        int hour = 0,
        int minute = 0,
        int second = 0,
        int millisecond = 0,
        int microsecond = 0])
```



## 函数类型

<mark style="color:blue;background-color:blue;">typedef</mark>把函数当做对象来看待

```dart

typedef Operation = double Function(double);

main() {
  //声明Operation类型的变量，指代square函数
  Operation op = square;
  print(op(10));
  print(op.call(10));
  op = cube;
  print(op(10));
}

double square(double a) {
  return a * a;
}

double cube(double a) => a * a * a;

```

函数作为入参

```dart
typedef Operation = double Function(double);

main() {
  double r1 = add(3, 4);
  print(r1);

  double r2 = add(3, 4, op: square);
  print(r2);

  //匿名函数
  double r3 = add(3, 4, op: (double e) => e * e * e);
  print(r3);
}

//函数作为可选入参
double add(double a, double b, {Operation? op}) {
  if (op == null) return a + b;
  return op(a) + op(b);
}

double square(double a) {
  return a * a;
}


```

## 异步任务

### <mark style="color:blue;background-color:blue;">Feture</mark>&#x20;

* `Future` `then`&#x20;
* `async/await`&#x20;

```dart
import 'dart:io';

import 'package:path/path.dart' as path;

/* doTask1()===开始读取====l10n.yaml===
doTask2()===开始读取====l10n.yaml===
doTask3
doTask1()===结束读取====l10n.yaml===
doTask1()===l10n.yaml内容: arb-dir: lib/timer/10/l10n/arb

template-arb-file: app_en.arb

output-localization-file: app_localizations.dart
doTask2()===结束读取====l10n.yaml===
doTask2()===l10n.yaml内容: arb-dir: lib/timer/10/l10n/arb

template-arb-file: app_en.arb

output-localization-file: app_localizations.dart */
void main() {
  doTask1();
  doTask2();
  doTask3();
}

void doTask1() {
  File file = File(path.join(Directory.current.path, "l10n.yaml"));
  print('doTask1()===开始读取====l10n.yaml===');
  file.readAsString().then((value) {
    print('doTask1()===结束读取====l10n.yaml===');
    print('doTask1()===l10n.yaml内容: $value');
  });
}

void doTask2() async {
  File file = File(path.join(Directory.current.path, "l10n.yaml"));
  print('doTask2()===开始读取====l10n.yaml===');
  String content = await file.readAsString();
  print('doTask2()===结束读取====l10n.yaml===');
  print('doTask2()===l10n.yaml内容: $content');
}

void doTask3() {
  print('doTask3');
}

```

### <mark style="color:blue;background-color:blue;">Stream</mark>&#x20;

`Stream#listen` 方法会返回一个 `StreamSubscription` 的订阅对象，通过该对象可以控制流的监听

> subscription.cancel();
>
> subscription.pause();&#x20;
>
> subscription.resume();

```dart
import 'dart:async';
import 'dart:io';

import 'package:path/path.dart' as path;

void main() {
  doTask1();
  doTask2();
  doTask3();
}

late StreamSubscription<List<int>> subscription;
int fileLength = 0;
int counter = 0;

void doTask2() async {
  File file =
      File(path.join(Directory.current.path, "assets", "Jane Eyre.txt"));
  print("开始读取 Jane Eyre.txt ");
  fileLength = await file.length();
  Stream<List<int>> stream = file.openRead();
  subscription = stream.listen(_onData, onDone: _onDone);
}

void _onData(List<int> bytes) async {
  counter += bytes.length;
  double progress = counter * 100 / fileLength;
  DateTime time = DateTime.now();
  String timeStr =
      "[${time.hour}:${time.minute}:${time.second}:${time.millisecond}]";
  print(timeStr + "=" * (progress ~/ 2) + '[${progress.toStringAsFixed(2)}%]');
  if (progress >= 50) {
    subscription.cancel();
  }
}

void _onDone() {
  print("读取 Jane Eyre.txt 结束");
}

void doTask1() {
  print('doTask1');
}

void doTask3() {
  print('doTask3');
}
```
