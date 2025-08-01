# StringBuilder in Java

## 🔹 What is `StringBuilder`?

* In Java, `String` is **immutable** — once created, it **cannot be changed**.
* `StringBuilder` is a **mutable** class — it allows you to **modify a string without creating a new object** every time.

### Why use `StringBuilder` instead of `String`?

Because it's **faster** and **memory efficient**, especially when:

* You're doing a lot of **string concatenation inside loops**.
* You're modifying strings frequently (insert, delete, reverse, etc.).

---

## 🔹 How to Create a StringBuilder

```java
StringBuilder sb = new StringBuilder();              // empty
StringBuilder sb2 = new StringBuilder("hello");      // with initial value
```

---

## 🔹 Commonly Used `StringBuilder` Methods

| Method                                  | Description                          | Example                    |
| --------------------------------------- | ------------------------------------ | -------------------------- |
| `append(String s)`                      | Adds string at the end               | `sb.append("world")`       |
| `insert(int offset, String s)`          | Inserts string at given index        | `sb.insert(2, "hi")`       |
| `replace(int start, int end, String s)` | Replaces part with another           | `sb.replace(0, 3, "hey")`  |
| `delete(int start, int end)`            | Deletes from start to end-1          | `sb.delete(0, 2)`          |
| `deleteCharAt(int index)`               | Deletes one character at index       | `sb.deleteCharAt(3)`       |
| `reverse()`                             | Reverses the string                  | `sb.reverse()`             |
| `toString()`                            | Converts `StringBuilder` to `String` | `String s = sb.toString()` |
| `length()`                              | Returns current length               | `sb.length()`              |
| `charAt(index)`                         | Returns character at index           | `sb.charAt(0)`             |
| `setCharAt(index, char)`                | Sets character at index              | `sb.setCharAt(1, 'a')`     |

---

## 🔹 Example Program

```java
public class Demo {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("hello");

        sb.append(" world");               // "hello world"
        sb.insert(5, ",");                 // "hello, world"
        sb.replace(0, 5, "hi");            // "hi, world"
        sb.delete(3, 5);                   // "hi world"
        sb.reverse();                      // "dlrow ih"
        
        System.out.println(sb);            // Output: dlrow ih
    }
}
```

---

## 🔹 Difference Between `String`, `StringBuilder`, `StringBuffer`

| Feature     | `String`                    | `StringBuilder`           | `StringBuffer`                             |
| ----------- | --------------------------- | ------------------------- | ------------------------------------------ |
| Mutability  | Immutable                   | Mutable                   | Mutable                                    |
| Thread-safe | Yes (by nature)             | No                        | Yes                                        |
| Performance | Slow (for multiple changes) | Fast                      | Slower than StringBuilder                  |
| Use Case    | When string doesn't change  | When string changes a lot | When string changes & thread safety needed |
