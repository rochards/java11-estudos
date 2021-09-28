# Estudos de Java 11
Estudos de Java 11 baseados no livro **OCP Complete Study Guide**


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

#### Classes genéricas

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

#### Interfaces genéricas
