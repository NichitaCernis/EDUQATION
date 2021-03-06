## Наследование классов. Статика




* Предположим есть базовый класс (super class), который содержит метод умеющий выводить на экран знак "#" - **drawHash()**, выводящий пробел - **drawSpace()**, а так же переносящий на новую строку **newLine()**
  
```java
class Shape {
    static void drawHash() {
        System.out.print("#");
    }
    static void drawSpace() {
        System.out.print(" ");
    }
    static void newLine() {
        System.out.print("\n");
    }
}
```

* У этого класса есть наследник **HorizontalLine** - который при помощи **drawLine()**, который использует наследованные методы от **Shape**, рисует горизонтальную линию указанной длины при помощи параметра **int line** 


```java
class HorizontalLine {
    static void drawLine(int length) {
        for(int i=0; i<length; i++){
            newLine();
            drawHash();
            newLine();
        }
    }
}
``` 

* Требуется:
  1.  Перезагрузить метод **drawLine(int length)** внутри класса **HorizontalLine**, так чтобы он смог быть вызван без параметров в скобках - но при этом - так чтобы он нарисовал линию с длиной в 5 знаков
  2.  Добавить еще одного наследника класса **Shape** - **VerticalLine**, который содержит два варианта метода **drawLine(...)** (c указанной высотой линии и без), эти методы должны нарисовать вертикальную линию
  3.  Добавить еще одного наследника класса **Shape** - **Rectangle**, который содержит два варианта метода **drawRect(...)** (c указанной высотой, шириной и без), эти методы должны нарисовать прямоугольник
* То есть если в **main()** написать


```java
HorizontalLine.drawLine(7);  
VerticalLine.drawLine(3);  
Rectangle.drawRect(4,4);
```
* то мы увидим

```

#######

#
#
#

####
####
####
####

```
