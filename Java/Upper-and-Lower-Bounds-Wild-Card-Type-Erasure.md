### Upper and Lower Bounds:

- **Upper Bound:** It restricts the type to be a subtype of a particular type.
  ```java
  class Box<T extends Number> {
      // T must be a subtype of Number
  }
  ```

- **Lower Bound:** It restricts the type to be a supertype of a particular type.
  ```java
  class Box<T super Integer> {
      // T must be a supertype of Integer
  }
  ```

### Wildcards:

- **Wildcard (`?`):** Represents an unknown type.
  ```java
  public void printList(List<?> list) {
      for (Object element : list) {
          System.out.println(element);
      }
  }
  ```

- **Upper Bounded Wildcard (`? extends T`):** Specifies that the unknown type must be a subtype of the specified type.
  ```java
  public double sum(List<? extends Number> list) {
      double sum = 0.0;
      for (Number number : list) {
          sum += number.doubleValue();
      }
      return sum;
  }
  ```

- **Lower Bounded Wildcard (`? super T`):** Specifies that the unknown type must be a supertype of the specified type.
  ```java
  public void addIntegers(List<? super Integer> list) {
      list.add(1);
      list.add(2);
      // Can add integers or superclasses of Integer
  }
  ```

### Type Erasure:

- **Type Erasure:** Java generics use type erasure during compilation to support backward compatibility with code written without generics.
- **How It Works:**
  - Generic types are replaced by their bound or the Object type.
  - Type parameters are removed at runtime.
  - Compiler inserts type casts as needed.
- **Example:**
  ```java
  public class Box<T> {
      private T value;

      public void setValue(T value) {
          this.value = value;
      }

      public T getValue() {
          return value;
      }
  }
  ```
  After type erasure, it becomes:
  ```java
  public class Box {
      private Object value;

      public void setValue(Object value) {
          this.value = value;
      }

      public Object getValue() {
          return value;
      }
  }
  ```

Type erasure allows generic code to interoperate with legacy code that doesn't use generics. However, it also means that generic type information is not available at runtime, limiting certain operations and checks that can be performed.
