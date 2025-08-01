# Java String Class - Most Useful Methods

Java's `String` is an **immutable** class (cannot be changed once created). Here's a categorized list of important methods:

## 1. Basic Methods

| Method             | Description                        | Example                          |
|--------------------|------------------------------------|----------------------------------|
| `length()`         | Returns the length of the string   | `"hello".length()` → `5`         |
| `charAt(index)`    | Returns char at given index        | `"hello".charAt(1)` → `'e'`      |
| `equals(str)`      | Checks if two strings are equal    | `"abc".equals("abc")` → `true`   |
| `equalsIgnoreCase(str)` | Case-insensitive comparison | `"Hello".equalsIgnoreCase("hello")` → `true` |
| `toLowerCase()`    | Converts to lowercase              | `"Java".toLowerCase()` → `"java"` |
| `toUpperCase()`    | Converts to uppercase              | `"java".toUpperCase()` → `"JAVA"` |
| `trim()`           | Removes leading/trailing spaces    | `" hello ".trim()` → `"hello"`   |
| `isEmpty()`        | Checks if length is 0              | `"".isEmpty()` → `true`          |

## 2. Comparison Methods

| Method                    | Description                          |
|---------------------------|--------------------------------------|
| `compareTo(str)`          | Lexicographically compares strings   |
| `compareToIgnoreCase(str)`| Ignores case while comparing         |

```java
"abc".compareTo("abd") → -1
"abc".compareToIgnoreCase("ABC") → 0
````
## 3. Search & Index Methods

| Method               | Description                  | Example                                |
|----------------------|------------------------------|----------------------------------------|
| `contains(substring)`| Checks if substring exists   | `"hello".contains("ll")` → `true`      |
| `indexOf(char/str)`  | First occurrence index       | `"hello".indexOf('l')` → `2`           |
| `lastIndexOf(char/str)` | Last occurrence index     | `"hello".lastIndexOf('l')` → `3`       |
| `startsWith(prefix)` | Checks beginning             | `"hello".startsWith("he")` → `true`    |
| `endsWith(suffix)`   | Checks ending                | `"hello".endsWith("lo")` → `true`      |

## 4. Substring & Replace Methods

| Method                    | Description                         | Example                                 |
|---------------------------|-------------------------------------|-----------------------------------------|
| `substring(start)`        | Returns substring from index        | `"hello".substring(2)` → `"llo"`        |
| `substring(start, end)`   | From start to end-1                 | `"hello".substring(1, 4)` → `"ell"`     |
| `replace(old, new)`       | Replaces all occurrences            | `"aabb".replace("a", "z")` → `"zzbb"`   |
| `replaceAll(regex, new)`  | Uses regex for replace              | `"abc123".replaceAll("[0-9]", "")` → `"abc"` |
| `replaceFirst(regex, new)`| Replaces first match only           | `"abc123abc".replaceFirst("a", "x")` → `"xbc123abc"` |

## 5. Conversion & Split

| Method             | Description                              |
|--------------------|------------------------------------------|
| `toCharArray()`    | Converts string to char array            |
| `split(delimiter)` | Splits string by regex or delimiter      |
| `valueOf(data)`    | Converts anything to string (e.g. int)   |

```java
String str = "Java is fun";
str.split(" ") → ["Java", "is", "fun"]
String.valueOf(123) → "123"

