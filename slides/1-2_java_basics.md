---
title: Java alapok
...


## Entry point

```java
class ProgramName {
    public static void main(String[] args) {
        System.out.println("Hello, World!"); 
    }
}
```

- minden `.java` source file legfeljebb egy `public` osztályt tartalmaz
- ha van public osztály, akkor a nevének egyezni kell a file nevével
- a `public static void main(String[] args)`-ként deklarált függvény a prorgam entry pointja

---

## Referenciák

> Minden referncia, kivéve ami nem

- Oogway

## Referencia típusok

```java
class DbConnection {
    public String path;

    DbConnection(String path) {
        this.path = path;
    }
}

class Main {
    public static void main(String[] args) {
        DbConnection db = new DbConnection("users.db");

        var db2 = db;

        System.out.println(db.path);
        System.out.println(db2.path);

        db2.path = "221B Baker Street";

        System.out.println(db.path);
        System.out.println(db2.path);
    }
}
```

. . .

A változók referenciák, nem értékek.

## Értéktípusok

```java
class Main {
    public static void main(String[] args) {
        int a = 5;
        int b = a;

        b = 10;
        System.out.println(a);


    }
}
```

. . .

Kivéve a primitív típusok, mivel ezek pont hogy értékek.

## Egyenlőség

So far, So good,... So what!?

```java  
class Main {
    public static void main(String[] args) {
        String a = new String("asd");
        String b = new String("asd");

        System.out.println(a == b);
    }
}
```
. . .

VS.

```java  
class Main {
    public static void main(String[] args) {
        String a = new String("asd");
        String b = new String("asd");

        System.out.println(a.equals(b));
    }
}
```

. . .

- az `==` operátor referencia-egyenlőséget vizsgál
- a `.equals()` metódus érték-egyenlőséget (vagy ahogy implementálva van)

## Bonus 

```java
import java.util.ArrayList;

class Main {
    public static void main(String[] args) {
        var lst1 = new ArrayList<StringBuffer>();
        var lst2 = new ArrayList<StringBuffer>();

        System.out.printf("lst1 == lst2 -> %s\n", lst1 == lst2);
        System.out.printf("lst1.equals(lst2) -> %s\n", lst1.equals(lst2));
    }
}
```

---

```java
    var sb = new StringBuffer("thats's ");
    lst1.add(sb);
    lst2.add(sb);
    
    System.out.printf("lst1: %s\n", lst1);
    System.out.printf("lst2: %s\n", lst2);
```

. . .

```java
    sb.append("bait");

    System.out.printf("lst1: %s\n", lst1);
    System.out.printf("lst2: %s\n", lst2);
```

. . .

```java
    sb = null;

    System.out.printf("lst1: %s\n", lst1);
    System.out.printf("lst2: %s\n", lst2);
```

