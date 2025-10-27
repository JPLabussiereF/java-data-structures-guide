# TreeSet

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

TreeSet é uma implementação de Set baseada em TreeMap (Red-Black Tree) que mantém elementos ordenados.

## 🔍 Características

- Baseado em TreeMap (Red-Black Tree balanceada)
- Mantém ordem natural ou por Comparator
- Não permite duplicatas
- NÃO permite null
- Não é thread-safe

## ⚖️ Trade-offs

### ✅ Vantagens
- Elementos sempre ordenados
- Operações O(log n) garantidas
- Suporta range queries (subSet, headSet, tailSet)
- Acesso ao menor/maior elemento O(log n)

### ❌ Desvantagens
- Mais lento que HashSet - O(log n) vs O(1)
- Maior uso de memória
- Requer elementos Comparable ou Comparator
- Não permite null

## 📊 Complexidade

| Operação | Complexidade |
|----------|--------------|
| add | O(log n) |
| remove | O(log n) |
| contains | O(log n) |
| first/last | O(log n) |

## 💻 Exemplos

```java
import java.util.*;

public class TreeSetExemplo {
    public static void main(String[] args) {
        // Ordem natural
        TreeSet<Integer> numeros = new TreeSet<>();
        numeros.add(5);
        numeros.add(1);
        numeros.add(3);
        
        System.out.println(numeros); // [1, 3, 5] - ordenado!
        
        // Primeiro e último
        System.out.println("Menor: " + numeros.first()); // 1
        System.out.println("Maior: " + numeros.last()); // 5
        
        // Range queries
        System.out.println("Menores que 4: " + numeros.headSet(4)); // [1, 3]
        System.out.println("Maiores ou iguais a 3: " + numeros.tailSet(3)); // [3, 5]
        
        // Comparator customizado (ordem reversa)
        TreeSet<Integer> reverso = new TreeSet<>(Collections.reverseOrder());
        reverso.addAll(Arrays.asList(5, 1, 3));
        System.out.println(reverso); // [5, 3, 1]
    }
}
```

## 🎯 Quando Usar

- Precisa de elementos ordenados
- Range queries são necessárias
- Acesso frequente a min/max
- Não se importa com O(log n)

---

[← Voltar ao Índice](../README.md)
