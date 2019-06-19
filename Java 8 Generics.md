# Java 8 Generics

## Generic and Inheritance

`List<Object>` is **not** the parent of `List<String>`

## Unbounded Wildcards

To declare and use a list of unbounded type:

```Java
List<?> stuff = Arrays.asList("Hello", LocalDate.now(), 3);

System.out.println(stuff.size());
stuff.forEach((Object o) -> System.out.println(o));

// However, stuff.add(...) won't compile
```

_The `?` means unknown type._

## Upper-Bounds

Syntax: `? extends T`

```Java
// The method to calculate the sum of list of numbers
public double sumList(List<? extends Number> list) {
  return list.stream()
          .mapToDouble(Number::doubleValue)
          .sum();
}

public void test() {
  List<Integer> ints = Arrays.asList(1, 2, 3, 4, 5);
  List<Double> doubles = Arrays.asList(1.1, 2.2, 3.3, 4.4, 5.5);
  double sum1 = sumList(ints);
  double sum2 = sumList(doubles);
}
```

Upper bound `? extends T` in Java is `covariant`, which preserve the ordering of types
from more specific to more general.

## Lower-Bounds

Syntax: `? super T`

```Java
// From java.lang.Iterable
default void forEach(Consumer<? super T> action) {
  Objects.requireNonNull(action);
  for (T t : this) {
    action.accept(t);
  }
}
```

Using forEach on a collection Strings, the T can be either String or Object

```Java
List<String> strings = Arrays.asList("a", "few", "strings");

strings.forEach((String s) -> System.out.println(s.toUpperCase()));
strings.forEach((Object o) -> System.out.println(s.hashCode()));
```

Lower bound `? super T` in Java is `contravariant', which preserve the ordering of types
from more general to more specific.

Rules:

- Use `extends` when consuming the values
- Use `super` when providing the values
- Use explicit type when do both

In Java 8 streams,

- to provide a value from the stream -> `super`
- to use the supplied value in lambda -> `extends`
