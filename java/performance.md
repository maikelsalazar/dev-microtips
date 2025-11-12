# ⚡ Java Performance Tips

## 📑 Table of Contents
- [Prefer `StringBuilder` or `StringBuffer` over `+` for concatenation](#prefer-stringbuilder-or-stringbuffer-over--for-concatenation)

## Prefer `StringBuilder` or `StringBuffer` over `+` for concatenation

In Java, strings are **inmutable**, meaning every concatenation with the `+` operator creates a new `String` **object**.

This leads to unnecessary memory allocation and garbage collection overhead, especially in loops or large concatenations.

`StringBuilder` (non-thread-safe) and `StringBuffer` (thread-safe) provide **mutable string manipulation**, which makes
them much faster in performance-critical sections


```java
// ✅ Faster — uses mutable buffer
StringBuilder sb = new StringBuilder();
sb.append("Hello");
sb.append(" ");
sb.append("World!");

System.out.println(sb.toString());

// ❌ Slower — creates multiple intermediate String objects
String message = "Hello" + " " + "World!";
System.out.println(message);
```

## 📊 Impact

The difference becomes significant when concatenating strings inside loops or when building large outputs (e.g., logs, reports, HTML, JSON).

```java
// ❌ Inefficient
String text = "";
for (int i = 0; i < 10000; i++) {
    text += i; // creates a new String every iteration
}

// ✅ Efficient
StringBuilder textBuilder = new StringBuilder();
for (int i = 0; i < 10000; i++) {
    textBuilder.append(i);
}
String text = textBuilder.toString();
```

## 💡 Rule of thumb
- Use `StringBuilder` in single-threaded contexts.
- Use `StringBuffer` in multi-threaded contexts.
- Avoid `+` concatenation in loops or performance-sensitive code.
- In modern Java (since Java 9+), the compiler optimizes some `+` operations.
but `StringBuilder` still wins in explicit, repeated concatenation scenarios.