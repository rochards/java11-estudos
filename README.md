# Estudos de Java 11
Estudos de Java 11 baseados no livro **OCP Complete Study Guide**


## Capítulo 14
### Working with Generics

Genéricos surgiram para forçar que se trabalhe com apenas um tipo de dado, como por exemplo:
```java
List<String> names = new ArrayList<>(); // só pode receber strings
names.add("Peter Parker"); // ok
names.add(new StringBuilder("Webbi")); // não compila
```

Convenção de nomes para *Generics*:
* `E` para um elemento;
* `K` para key de map;
* `V` para valor de map;
* `N` para um número;
* `T` para um tipo de dado genérico;
* `S`, `U`, `V` e assim por diante, para múltiplos tipos genéricos.