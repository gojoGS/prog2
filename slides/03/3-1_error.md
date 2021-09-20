---
title: "Lesson 03.1: Error-handling"
---

# The Bad

```java
public static String garbage(String path) {
    var reader = new BufferedReader(new FileReader(path));

    return reader.readLine();
}
```
. . .

Le sem fordul

---

# rethrow

```java
public static String mayThrow(String path) throws IOException {
    var reader = new BufferedReader(new FileReader(path));

    return reader.readLine();
}
```

. . .

A hívónak kell kezelni az exceptiont.

---

# try-catch

```java
public static String wontThrow(String path)  {
    BufferedReader reader = null;

    try {
        reader = new BufferedReader(new FileReader(path));
    } catch (FileNotFoundException e) {
        return null;
    }

    try {
        return reader.readLine();
    } catch (IOException e) {
        return null;
    }
}
```

. . .

Ha a hiba kezelhező lokálisan, akkor kezeljük lokálisan.

---

# Egy másik példa

```java
public static int readInt(String path)  {
    Scanner contents = new Scanner(new File(path));
    return Integer.parseInt(contents.nextLine());
}
```

. . .

```java
public static int readInt(String path)  {
    try {
        Scanner contents = new Scanner(new File(path));
        return Integer.parseInt(contents.nextLine());
    } catch (FileNotFoundException e) {
        return 0;
    } catch (NumberFormatException e) {
        return 0;
    }
}
```

. . .

```java
public static int readInt(String path)  {
    try {
        Scanner contents = new Scanner(new File(path));
        return Integer.parseInt(contents.nextLine());
    } catch (FileNotFoundException | NumberFormatException e) {
        return 0;
    }
}
```

. . .

```java
public static Optional<Integer> readInt(String path)  {
    try {
        Scanner contents = new Scanner(new File(path));
        return Optional.of(Integer.parseInt(contents.nextLine()));
    } catch (FileNotFoundException | NumberFormatException e) {
        return Optional.empty();
    }
}
```

---

# Finally

```java
public static int mayThrow(String path) {
    Scanner contents = null;
    try {
        contents = new Scanner(new File(path));
        return Integer.parseInt(contents.nextLine());
    } catch (FileNotFoundException e) {
        return 0;
    } finally {
        if (contents != null) {
            contents.close();
        }
    }
}
```

. . .

Mi van ha a finally-ban is dobhat valami errort?

---

# Try-with-resource

```java
public static int mayThrow(String path) {
    try (Scanner contents = new Scanner(new File(path))) {
        return Integer.parseInt(contents.nextLine());
    } catch (FileNotFoundException e) {
        return 0;
    }
}
```

. . .

Szükséges hozzá az `AutoCloseable` interfész implementálása.

---

# Anti-patterns

```java
public static int mayThrow(String s) throws IOException {
    if (s.equals("nem")) {
        return 0;
    } else {
        throw new IOException();
    }
}
```

---

```java
public static int mayGetThrown() {
    try {
        var i = mayThrow("lol");
        return i;
    } catch (IOException e) { }

    return -1;
}
```

. . .

```java
public static int mayGetThrown() {
    try {
        var i = mayThrow("lol");
        return i;
    } catch (IOException e) {
        // sose fog ez történni
    }

    return -1;
}
```

. . .

```java
public static int mayGetThrown() {
    try {
        var i = mayThrow("lol");
        return i;
    } catch (IOException e) {
        e.printStackTrace();
    }

    return -1;
}
```

. . .

```java
public static int mayGetThrown() throws DidntSayNoException {
    try {
        var i = mayThrow("lol");
        return i;
    } catch (IOException e) {
        throw new DidntSayNoException("nem mondta hogy nem a foga fáj");
    }
}
```

---

```java
public int foo() {
    int i = 0;
    try {
        throw new IOException();
    } finally {
        return i; // <--
    }
}
```

. . .

Elnyelődik az Exception

---

```java
public int foo() throws DidntSayNoException {
    try {
        throw new IOException();
    } catch ( IOException io ) {
        throw new IllegalStateException(io); // <==
    } finally {
        throw new DidntSayNoException("asd");
    }
}
```

. . .

Elnyelődik az Exception
