---
title: Java alapok
...



# Entry point

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

# Referenciák

> Minden referncia, kivéve ami nem

- Oogway

---

# Referencia típusok

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

---


# Értéktípusok

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

---

# Egyenlőség

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

---

# Bonus 

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

---

## for

```java
class Main {
    public static void main(String[] args) {
        for(int i = 0; i < 1; ++i) {
            System.out.println("Ugyanat mint C++-ban");
        }
    }
}
```

---

## while

```java
class Main {
    public static void main(String[] args) {
        while(true) {
            System.out.println("Ugyanat mint C++-ban");
        }
    }
}
```

---

## foreach

```java
import java.util.List;

class Main {
    public static void main(String[] args) {
        var poem = List.of(
                "Bőre illata paprika",
                "Népi naíva",
                "Azt mondta a neve Marika"
        );

        for (var line : poem) {
            System.out.println(line);
        }
    }
}
```

---

## class


---

## abstract class

```java
public abstract class Entity {
    private int maxHealth;
    private int health;
    private int level;

    protected Entity(int maxHealth, int level) {
        this.health = maxHealth;
        this.maxHealth = maxHealth;
        this.level = level;
    }

    void draw() {
        System.out.println("Graphics black magic");
    }
}
```

---

```java
abstract class Npc extends Entity {
    private static double strengthModifierBecauseItsEasierThanAi = 1.0;

    public static void setDifficultyModifier(double modifier) {
        strengthModifierBecauseItsEasierThanAi = modifier;
    }

    protected Npc(int maxHealth, int level) {
        super(maxHealth, level);
    }

    abstract void move();
}
```
. . . 

```java
class WhiteTowerWatchman extends Npc {
    WhiteTowerWatchman() {
        super(950, 15);
    }

    void move() {
        System.out.println("Help the player");
    }
}
```

```java
class Orc extends Npc {
    Orc() {
        super(50, 10);
    }

    void move() {
        System.out.println("Destroy the MTV Székház");
    }
}
```

---

```java
class Player extends Entity {
    int experience;

    protected Player() {
        super(9999, 1);
        this.experience = 0;
    }

    @Override
    void draw() {
        System.out.println("Graphics black magic: dont render model, use static image");
    }
}
```

---

```java
// main.java

class Main {
    public static void main(String[] args) {
        List<Entity> lst = List.of(
                new Orc(),
                new Orc(),
                new WhiteTowerWatchman(),
                new Orc(),
                new WhiteTowerWatchman(),
                new Player()
        );

        for (var entity : lst) {
            entity.draw();

            if (!(entity instanceof Player)) {
                ((Npc) entity).move();
            }
        }
    }
}
```

---

## interface

. . .

```java
interface Statement {
    // dolgok
}

interface Connection {
    /**
     * A constant indicating that transactions are not supported.A constant indicating that transactions are not supported.
     */
    static final int TRANSACTION_NONE = 0;

    boolean isValid(int timeout);

    boolean isClosed();

    Statement createStatement();

    void commit();

    void rollback();

    void close();

}
```

---

```java
class MysqlConnection implements Connection {

    @Override
    public boolean isValid(int timeout) {
        return true;
    }

    @Override
    public boolean isClosed() {
        return false;
    }

    @Override
    public Statement createStatement() {
        return null;
    }

    @Override
    public void commit() {
        System.out.println("Delete all the data");
    }

    @Override
    public void rollback() {
        System.out.println("Something bad");
    }

    @Override
    public void close() {
        System.out.println("Bye, Bye");
    }
}
```

---

```java
interface Iterator {
}

interface Iterable {
    void forEach();

    Iterator iterator();
}
```

. . .

```java
interface Collection {
    boolean add(Object o);

    void clear();

    boolean contains(Object o);

    boolean isEmpty();

    boolean remove(Object o);

}
```

. . .

```java
interface List {
    void add(int index, Object o);

    Object get(int index);

    int indexOf(Object o);
}
```

---

```java
class ArrayList
        implements Iterable, Collection, List {

    @Override
    public void forEach() { }

    @Override
    public Iterator iterator() { return null; }

    @Override
    public boolean add(Object o) { return false; }

    @Override
    public void clear() { }

    @Override
    public boolean contains(Object o) { return false; }

    @Override
    public boolean isEmpty() { return false; }

    @Override
    public boolean remove(Object o) { return false; }

    @Override
    public void add(int index, Object o) { }

    @Override
    public Object get(int index) { return null; }

    @Override
    public int indexOf(Object o) { return 0; }
}
```

---

## enum

```java
// Status.java

public enum Status {
    OK(200),
    FORBIDDEN(403),
    NOT_FOUND(404);

    private int code;

    Status(int i) {
        this.code = i;
    }

    boolean isStatusGood() {
        return this.code < 400;
    }

    boolean isStatusBad() {
        return !isStatusGood();
    }
}
```

---

```java
// Main.java

class Main {
    public static void main(String[] args) {
        var response = Status.OK;

        if (response.isStatusBad()) {
            System.out.println("I have a baaad feeling about this!");
        } else {
            System.out.println("everything seems OK");
        }
    }
}
```

---

## record

Más nyelvekben (ha van), akkor `dataclass`-nak is hívják.

```java
// Employee.java

public record Employee(int id, int income, double taxModifier) {
    public double calculatePay() {
        return income * taxModifier;
    }
}
```

. . .

```java
// Main.java

class Main {
    public static void main(String[] args) {
        Employee max = new Employee(0, 25000, 0.95);
        System.out.printf("id: %s pays %s", max.id(), max.calculatePay());
    }
}
```

---

A `record` osztályok:

- minden mező `private final`
- minden mezőnek van getter metódusa (`.fieldName()`)
- publikus konstruktor, minden mezőt bekérünk argomentumként
- alapértelmezetten `.equals()` metódus
- alapértelmezetten `.hashCode()` metódus
- alapértelmezetten `.toString()` metódus
- változtathatatlan/állandó (**immutable**) adattípus

---
