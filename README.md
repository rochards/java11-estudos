# Estudos de Java 11
Estudos de Java 11 baseados no livro **OCP Complete Study Guide**. Os títulos e subtítulos do livro foram mantidos em inglês para fácil localização no livro.


## Capítulo 14
### Working with Generics

Genéricos surgiram para que o programador consiga parametrizar o tipo de dado com que ele deseja trabalhar. Por exemplo, a interface `List` por ser parametrizada como se segue:
```java
List<String> names = new ArrayList<>(); // só vai poder receber strings
names.add("Peter Parker"); // ok
names.add(new StringBuilder("Webbi")); // não compila
```

Convenção de nomes para *Generics*:
* `E` para um elemento;
* `K` para key de um map;
* `V` para valor de um map;
* `N` para um número;
* `T` para um tipo de dado genérico;
* `S`, `U`, `V` e assim por diante, para múltiplos tipos genéricos.

#### Generics Classes

Por baixo dos panos o compilador substitui as referências genéricas por um `Object`. Quando fazemos:
```java
public class Crate<T> {
    private T content;
    public T emptyCrate() {
        return content;
    }
}
```
o compilador na verdade está fazendo:
```java
public class Crate {
    private Object content;
    public Object emptyCrate() {
        return content;
    }
}
```
e add os necessários *casts* para o código funcionar:
```java
// Robot é uma classe definida qualquer
Crate<Robot> crate = new Crate<>();
Robot r = (Robot) crate.emptyCrate(); // (Robot) é add implicitamente pelo compilador 
```

#### Generic Interfaces

```java
public interface Shippable<T> {
    void ship(T t);
}
```

Você pode implementar essa interface de duas formas:
* Ex1. com uma classe concreta:
  ```java
  // Robot abaixo seria uma classe qualquer
  public class ShippableRobotCrate implements Shippable<Robot> {
      void ship(Robot t) { /*...*/ }
  }
  ```
* Ex2. com uma classe abstrata:
  ```java
  // não compila se você não parametrizar tbm ShippableCrate
  public abstract class ShippableCrate<T> implements Shippable<T> {
      @Override
      void ship(T t) { /*...*/ }
  }
  ```

#### Generic Methods

Antes do retorno do método, nós formalmente declaramos o tipo genérico `<T>` (*formal parameter type*). Lembrando que `<T>` pode ser qualquer letra.
```java
public class More {
    public static <T> void sink() {/*...*/}
    public static <T> T identity(T t) { return t; }
    public static T noGood(T t) { return t; } // não compila pq o tipo genérico <T> não foi especificado
}
```

#### Bounding Generic Types

O livro descreve que um *bounded parameter type* é um tipo genérico que especifica uma restrição para os tipos de classes que determinado atributo `T` pode receber. 

O _**wildcard generic type**_ é representado pelo sinal de interrogação `?`.

Tipos de bounds:
| Tipo de bound | Sintaxe | Examplo |
| ------------- | ------ | ------- |
| Unbounded wildcard | `?` | `List<?> l = new ArrayList<String>();` |
| Wildcard with an upper bound | `? extends type` | `List<? extends Exception> l = new ArrayList<RuntimeException>();` |
| Wildcard with a lower bound | `? super type` | `List<? super Exception> l = new ArrayList<Object>();` |
