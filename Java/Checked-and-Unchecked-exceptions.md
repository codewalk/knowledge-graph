**Checked Exceptions:**

Checked exceptions are exceptions that the Java compiler requires you to handle explicitly. They are checked at compile-time, and if not caught or declared, the code will not compile.

1. **`IOException`:**
   - Represents an error during I/O operations.
   - Examples: `FileNotFoundException`, `IOException`, `EOFException`.

```java
try {
    // Code that may throw IOException
    FileReader fileReader = new FileReader("file.txt");
    // ...
} catch (IOException e) {
    // Handle or log the exception
    e.printStackTrace();
}
```

2. **`SQLException`:**
   - Indicates an error with database access.
   - Examples: `SQLException`, `SQLDataException`.

```java
try {
    // Code that may throw SQLException
    Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydatabase", "user", "password");
    // ...
} catch (SQLException e) {
    // Handle or log the exception
    e.printStackTrace();
}
```

**Unchecked Exceptions (Runtime Exceptions):**

Unchecked exceptions are exceptions that are not checked at compile-time. They usually result from programming errors and can be caught and handled, but the compiler does not enforce handling them.

1. **`ArithmeticException`:**
   - Occurs when an arithmetic operation encounters an exceptional condition.
   - Examples: Division by zero.

```java
int result;
try {
    result = 10 / 0; // ArithmeticException
} catch (ArithmeticException e) {
    // Handle or log the exception
    e.printStackTrace();
}
```

2. **`NullPointerException`:**
   - Occurs when attempting to access an object or invoke a method on a null reference.
   - Examples: Trying to call a method on a null object.

```java
String str = null;
try {
    int length = str.length(); // NullPointerException
} catch (NullPointerException e) {
    // Handle or log the exception
    e.printStackTrace();
}
```

3. **`ArrayIndexOutOfBoundsException`:**
   - Occurs when trying to access an array element with an illegal index.
   - Examples: Accessing an array element beyond its bounds.

```java
int[] array = {1, 2, 3};
try {
    int value = array[5]; // ArrayIndexOutOfBoundsException
} catch (ArrayIndexOutOfBoundsException e) {
    // Handle or log the exception
    e.printStackTrace();
}
```

4. **`NumberFormatException`:**
   - Occurs when parsing a string that is not a valid representation of a number.
   - Examples: Trying to parse a non-numeric string.

```java
String str = "abc";
try {
    int number = Integer.parseInt(str); // NumberFormatException
} catch (NumberFormatException e) {
    // Handle or log the exception
    e.printStackTrace();
}
```

In general, checked exceptions are used for situations where the code can anticipate and recover from an exceptional condition, while unchecked exceptions are typically used for programming errors or conditions that are harder to predict.
