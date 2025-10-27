# PriorityQueue (Heap)

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

PriorityQueue é uma fila baseada em heap binário que mantém elementos ordenados por prioridade.

## 🔍 Características

- Implementada como min-heap (ou max-heap com comparator)
- NÃO é FIFO - elementos saem por prioridade
- Não permite null
- Não é thread-safe
- Array-based heap

## ⚖️ Trade-offs

### ✅ Vantagens
- Acesso ao menor/maior elemento O(1)
- Inserção e remoção O(log n)
- Ideal para Top K, Dijkstra, A*
- Uso eficiente de memória

### ❌ Desvantagens
- Sem acesso aleatório
- Contains é O(n)
- Iteração não é ordenada
- Remove arbitrário é O(n)

## 📊 Complexidade

| Operação | Complexidade |
|----------|--------------|
| offer/add | O(log n) |
| poll/remove | O(log n) |
| peek | O(1) |
| contains | O(n) |

## 💻 Exemplos

### Exemplo 1: Min-Heap

```java
import java.util.*;

public class MinHeapExemplo {
    public static void main(String[] args) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        
        minHeap.offer(5);
        minHeap.offer(1);
        minHeap.offer(3);
        
        while (!minHeap.isEmpty()) {
            System.out.println(minHeap.poll());
        }
        // Output: 1, 3, 5 (ordem crescente)
    }
}
```

### Exemplo 2: Max-Heap

```java
import java.util.*;

public class MaxHeapExemplo {
    public static void main(String[] args) {
        // Max-heap com comparador reverso
        PriorityQueue<Integer> maxHeap = 
            new PriorityQueue<>(Collections.reverseOrder());
        
        maxHeap.offer(5);
        maxHeap.offer(1);
        maxHeap.offer(3);
        
        while (!maxHeap.isEmpty()) {
            System.out.println(maxHeap.poll());
        }
        // Output: 5, 3, 1 (ordem decrescente)
    }
}
```

### Exemplo 3: K Maiores Elementos

```java
import java.util.*;

public class KMaioresElementos {
    public static List<Integer> kMaiores(int[] nums, int k) {
        // Min-heap de tamanho k
        PriorityQueue<Integer> heap = new PriorityQueue<>();
        
        for (int num : nums) {
            heap.offer(num);
            if (heap.size() > k) {
                heap.poll(); // Remove o menor
            }
        }
        
        return new ArrayList<>(heap);
    }
    
    public static void main(String[] args) {
        int[] nums = {3, 2, 1, 5, 6, 4};
        System.out.println("3 maiores: " + kMaiores(nums, 3));
        // [4, 5, 6]
    }
}
```

### Exemplo 4: Merge K Sorted Lists

```java
import java.util.*;

class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

public class MergeKLists {
    public static ListNode mergeKLists(ListNode[] lists) {
        PriorityQueue<ListNode> heap = new PriorityQueue<>(
            (a, b) -> a.val - b.val
        );
        
        // Adiciona primeiro nó de cada lista
        for (ListNode node : lists) {
            if (node != null) {
                heap.offer(node);
            }
        }
        
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        
        while (!heap.isEmpty()) {
            ListNode node = heap.poll();
            tail.next = node;
            tail = tail.next;
            
            if (node.next != null) {
                heap.offer(node.next);
            }
        }
        
        return dummy.next;
    }
}
```

## 🎯 Quando Usar

- Top K elementos
- Median finding
- Algoritmos de grafos (Dijkstra, A*)
- Scheduling por prioridade
- Merge K sorted arrays/lists

---

[← Voltar ao Índice](../README.md)
