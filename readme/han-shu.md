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
