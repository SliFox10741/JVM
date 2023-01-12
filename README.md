# JVM

Код для исследования:
```java
public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}
```
При запуске программу в ClassLoader для дальнейшей загрузки поступает класс JvmComprehension, данные о котором, в дальнейшем, попадают в Metaspace.
В Stack Memory создается новый фрейм main;
```java
public class JvmComprehension {
    public static void main(String[] args) {
```
1) В фрейм main загружается переменная типа int 'i', равная 1:
```java
int i = 1;
```
2) В heap выделяется место под объект o типа Object. В фрейме main создается ссылка на него:
```java
Object o = new Object();
```
3) В heap выделяется место под объект 'ii' типа Integer. В фрейме main создается ссылка на него. Так происходит потому что в отличии от переменной i (она относится к int - примитивный тип), переменная 'ii' типа Integer - это класс-оболочка, соответствующий int:
```java
Integer ii = 2;
```
4) В Stack Memory создается новый фрейм printAll. В данный фрейм передаются значения o, i и ii:
```java
printAll(o, i, ii);
```
5) В heap выделяется место под объект uselessVarтипа типа Integer, с значением, равным 700. В фрейме printAll создается ссылка на него:
```java
Integer uselessVar = 700;
```
6) В Stack Memory создаются фреймы println и toString. В фрейм println передаются переменная i = 1, а так же переменные ii, которые хранят ссылки на объекты o и ii. Затем Garbage Collection удаляет ссылочную переменную o:
```java
System.out.println(o.toString() + i + ii);
```
7) В heap выделяется место под объект типа String ("finished"). В фрейме println создается ссылка на него: 
```java
System.out.println("finished");
```
