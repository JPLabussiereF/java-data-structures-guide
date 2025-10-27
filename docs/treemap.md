# TreeMap

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

TreeMap é uma implementação de Map baseada em Red-Black Tree que mantém chaves ordenadas.

## 🔍 Características

- Baseado em Red-Black Tree (auto-balanceada)
- Chaves sempre ordenadas
- NÃO permite chave null (mas permite valores null)
- Não é thread-safe

## ⚖️ Trade-offs

### ✅ Vantagens
- Chaves sempre ordenadas
- Operações O(log n) garantidas
- Range queries (subMap, headMap, tailMap)
- Acesso a menor/maior chave

### ❌ Desvantagens
- Mais lento que HashMap: O(log n) vs O(1)
- Maior uso de memória
- Requer chaves Comparable ou Comparator

## 📊 Complexidade

| Operação | Complexidade |
|----------|--------------|
| get | O(log n) |
| put | O(log n) |
| remove | O(log n) |
| containsKey | O(log n) |

## 💻 Exemplos

```java
import java.util.*;

public class TreeMapExemplo {
    public static void main(String[] args) {
        TreeMap<String, Integer> notas = new TreeMap<>();
        
        notas.put("Carlos", 85);
        notas.put("Alice", 95);
        notas.put("Bob", 75);
        
        // Iteração em ordem alfabética
        System.out.println(notas);
        // {Alice=95, Bob=75, Carlos=85}
        
        // Primeira e última chave
        System.out.println("Primeiro: " + notas.firstKey()); // Alice
        System.out.println("Último: " + notas.lastKey()); // Carlos
        
        // Range queries
        System.out.println("A-B: " + notas.headMap("C")); // {Alice=95, Bob=75}
        
        // Floor e Ceiling
        System.out.println("Floor de 'Brenda': " + notas.floorKey("Brenda")); // Bob
        System.out.println("Ceiling de 'Brenda': " + notas.ceilingKey("Brenda")); // Carlos
    }
}
```

### Exemplo: Top K Elementos

```java
import java.util.*;

public class TopKElementos {
    public static List<Integer> topK(int[] nums, int k) {
        TreeMap<Integer, Integer> freq = new TreeMap<>();
        
        // Conta frequências
        for (int num : nums) {
            freq.put(num, freq.getOrDefault(num, 0) + 1);
        }
        
        // Pega top K
        PriorityQueue<Map.Entry<Integer, Integer>> pq = 
            new PriorityQueue<>((a, b) -> b.getValue() - a.getValue());
        pq.addAll(freq.entrySet());
        
        List<Integer> result = new ArrayList<>();
        for (int i = 0; i < k && !pq.isEmpty(); i++) {
            result.add(pq.poll().getKey());
        }
        
        return result;
    }
    
    public static void main(String[] args) {
        int[] nums = {1, 1, 1, 2, 2, 3};
        System.out.println("Top 2: " + topK(nums, 2)); // [1, 2]
    }
}
```

## 🎯 Quando Usar

- Precisa de chaves ordenadas
- Range queries por chave
- Problemas de intervalos
- Acessos frequentes a min/max

---

[← Voltar ao Índice](../README.md)
