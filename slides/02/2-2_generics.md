---
title: "Lesson 02.2: Java generics"
---

# Non-generic példa

```java
public class StringArrayList {
    private String[] data;
    private int size;
    private int capacity;

    StringArrayList() {
        this.data = new String[1];
        this.capacity = 1;
        this.size = 0;
    }

}
```

---

```java
void add(String s) {
    if (size == capacity) {
        capacity *= 2;

        var newData = new String[capacity];
        System.arraycopy(data, 0, newData, 0, size);

        data = newData;
    }

    data[size++] = s;
}
```

. . .

```java
boolean contains(String s) {
    for(var elem : data) {
        if (elem.equals(s)) {
            return true;
        }
    }

    return false;
}
```

. . .

```java
@Override
public String toString() {
    var sb = new StringBuilder("[");

    var sj = new StringJoiner(", ");
    for(int i = 0; i < size; ++i) {
        sj.add(data[i]);
    }
    
    return sb.append(sj).append("]").toString();
}
```

---

# Generic példa

```java
public class ArrayList<T> {
    private T[] data;
    private int size;
    private int capacity;

    ArrayList() {
        this.data = (T[]) new Object[1];
        this.capacity = 1;
        this.size = 0;
    }
}
```

---

```java
void add(T s) {
    if (size == capacity) {
        capacity *= 2;

        var newData = (T[]) new Object[capacity];
        System.arraycopy(data, 0, newData, 0, size);

        data = newData;
    }

    data[size++] = s;
}
```

. . .

```java
boolean contains(T s) {
    for(var elem : data) {
        if (elem.equals(s)) {
            return true;
        }
    }

    return false;
}
```

. . .

```java
@Override
public String toString() {
    var sb = new StringBuilder("[");

    var sj = new StringJoiner(", ");
    for(int i = 0; i < size; ++i) {
        sb.append(data[i]);
    }

    return sb.append(sj).append("]").toString();
}
```
---

# Wildcards

## Unbounded wildcard

```java
public static void printAnyList(List<?> lst) {
    for(var elem: lst) {
        System.out.println(elem);
    }
}
public static void main(String[] args) {
    printAnyList(List.of(1, 2, 3));

    printAnyList(List.of(
            new String("asd")
    ));

    printAnyList(List.of(
            new Double(3.121)
    ));
}
```

---

## Upper bounded wildcard

```java
public static double sumList(List<? extends Number> lst) {
    double sum = 0.0;

    for(var elem: lst) {
        sum += elem.doubleValue();
    }

    return sum;
}

public static void main(String[] args) {
    var sum1 = sumList(
            List.of(1, 2, 3, 4)
    );

    System.out.println(sum1);

    var sum2 = sumList(
            List.of(1.12, 4.1231, 5.34)
    );

    System.out.println(sum2);
}
```
. . .

A wildcard egy típust jelöl, ami vagy `Number`, vagy `Number` valamely alosztálya.

---

```java
public abstract class DeepCopyCollection<E extends Cloneable>{
    // metódusok
}
```

---

## Lower bounded wildcard

```java
public static void foo(List<? super Integer> lst) {
        
}
```

A wildcard egy típust jelöl, ami vagy `Integer`, vagy integer valamely szülője.

---

## multiple, bound

```java
class AbstractCollection{}
interface Comparable {}

public class Foo <T extends AbstractCollection & Comparable>{
    T comparableCollection;
}
```