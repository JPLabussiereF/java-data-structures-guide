# HashSet

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

HashSet é uma implementação de Set baseada em HashMap, que não permite elementos duplicados e não mantém ordem.

## 🔍 Características

- Baseado em HashMap (internamente usa HashMap<E, Object>)
- NÃO permite duplicatas
- NÃO mantém ordem de inserção
- Permite um elemento null
- Não é thread-safe

## ⚖️ Trade-offs

### ✅ Vantagens
- Operações O(1) em média para add, remove, contains
- Rápido para verificar existência
- Ideal para eliminar duplicatas
- Baixo uso de memória (comparado a TreeSet)

### ❌ Desvantagens
- Sem ordem garantida
- Performance degrada para O(n) com colisões
- Requer boa implementação de hashCode()
- Uso de memória maior que array

## 📊 Complexidade

| Operação | Média | Pior Caso |
|----------|-------|-----------|
| add | O(1) | O(n) |
| remove | O(1) | O(n) |
| contains | O(1) | O(n) |
| Iteração | O(n) | O(n) |

## 💻 Exemplos Práticos

### Exemplo 1: Operações Básicas

```java
import java.util.HashSet;
import java.util.Set;

public class HashSetBasico {
    public static void main(String[] args) {
        Set<String> nomes = new HashSet<>();
        
        // Add O(1)
        nomes.add("Alice");
        nomes.add("Bob");
        nomes.add("Carlos");
        nomes.add("Alice"); // Duplicata ignorada
        
        System.out.println("Tamanho: " + nomes.size()); // 3
        
        // Contains O(1)
        System.out.println("Contém Bob? " + nomes.contains("Bob"));
        
        // Remove O(1)
        nomes.remove("Bob");
        
        // Iteração - ordem não garantida!
        for (String nome : nomes) {
            System.out.println(nome);
        }
    }
}
```

### Exemplo 2: Remover Duplicatas de Lista

```java
import java.util.*;

public class RemoverDuplicatas {
    public static <T> List<T> removerDuplicatas(List<T> lista) {
        // O(n) - muito eficiente
        return new ArrayList<>(new HashSet<>(lista));
    }
    
    public static void main(String[] args) {
        List<Integer> numeros = Arrays.asList(1, 2, 2, 3, 4, 4, 5);
        List<Integer> unicos = removerDuplicatas(numeros);
        
        System.out.println("Original: " + numeros);
        System.out.println("Sem duplicatas: " + unicos);
    }
}
```

### Exemplo 3: Operações de Conjunto

```java
import java.util.HashSet;
import java.util.Set;

public class OperacoesConjunto {
    public static void main(String[] args) {
        Set<Integer> a = new HashSet<>(Set.of(1, 2, 3, 4, 5));
        Set<Integer> b = new HashSet<>(Set.of(4, 5, 6, 7, 8));
        
        // União
        Set<Integer> uniao = new HashSet<>(a);
        uniao.addAll(b);
        System.out.println("União: " + uniao); // [1,2,3,4,5,6,7,8]
        
        // Interseção
        Set<Integer> intersecao = new HashSet<>(a);
        intersecao.retainAll(b);
        System.out.println("Interseção: " + intersecao); // [4,5]
        
        // Diferença
        Set<Integer> diferenca = new HashSet<>(a);
        diferenca.removeAll(b);
        System.out.println("Diferença A-B: " + diferenca); // [1,2,3]
    }
}
```

### Exemplo 4: Encontrar Primeiro Caractere Não Repetido

```java
import java.util.*;

public class PrimeiroNaoRepetido {
    public static Character primeiroUnico(String str) {
        Set<Character> unicos = new HashSet<>();
        Set<Character> duplicados = new HashSet<>();
        
        for (char c : str.toCharArray()) {
            if (duplicados.contains(c)) {
                continue;
            }
            if (unicos.contains(c)) {
                unicos.remove(c);
                duplicados.add(c);
            } else {
                unicos.add(c);
            }
        }
        
        // Primeira ocorrência única
        for (char c : str.toCharArray()) {
            if (unicos.contains(c)) {
                return c;
            }
        }
        
        return null;
    }
    
    public static void main(String[] args) {
        System.out.println(primeiroUnico("leetcode")); // l
        System.out.println(primeiroUnico("loveleetcode")); // v
    }
}
```

## 🎯 Quando Usar

- Eliminar duplicatas
- Verificação rápida de existência
- Operações de conjunto (união, interseção)
- Quando ordem não importa
- Cache de elementos visitados

## 🔗 Relacionados
- [LinkedHashSet](./linkedhashset.md) - Mantém ordem de inserção
- [TreeSet](./treeset.md) - Mantém ordem natural
- [HashMap](./hashmap.md) - Implementação base

---

[← Voltar ao Índice](../README.md)
