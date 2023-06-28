# 变量

## 不可变量：关键字<mark style="color:blue;background-color:blue;">const</mark>（编译时常量）和<mark style="color:blue;background-color:blue;">final</mark>（运行时常量）

````dart
```dart
main() {
  // t1不能再被赋值
  const String t1 = 't1'; 

  // 其他变量可以赋值给t2 (不推荐)
  final t2 = t1*2; 

  // t1 = t2;
}
```
````

## 可变量：默认数据类型和<mark style="color:blue;background-color:blue;">var</mark>&#x20;

## 数字<mark style="color:blue;background-color:blue;">num</mark> 类型是整形 <mark style="color:blue;background-color:blue;">int</mark> 和浮点型 <mark style="color:blue;background-color:blue;">double</mark> 的抽象类

````dart
```dart
main(){
  num a = 57;
  num b = 3.28;
  print("a:${a.runtimeType}===b:${b.runtimeType}");
}
```
````

## 字符串模版拼接

通过 `${变量}` 插入变量

````dart
```dart
main() {
  String addr = '逍遥津公园';
  String name = '小芳';
  String result = '今天我和${name}一起去$addr玩，很开心！';
  print(result);
}
```
````
