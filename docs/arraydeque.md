# ArrayDeque

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

ArrayDeque é uma implementação de Deque baseada em array circular redimensionável. É a implementação recomendada para pilhas e filas.

## 🔍 Características

- Array circular (mais eficiente que LinkedList)
- Cresce automaticamente (dobra de tamanho)
- NÃO permite elementos null
- Não é thread-safe
- Mais rápida que Stack e LinkedList

## ⚖️ Trade-offs

### ✅ Vantagens
- **Performance superior** a LinkedList e Stack
- Cache-friendly (localidade de memória)
- Menos overhead de memória
- Operações O(1) em ambas as pontas
- Substitui Stack com melhor performance

### ❌ Desvantagens
- Não permite null
- Redimensionamento ocasional O(n)
- Sem acesso eficiente ao meio
- Iteração pode ser mais complexa internamente

## 📊 Complexidade

| Operação | Complexidade |
|----------|--------------|
| addFirst/Last | O(1) amortizado |
| removeFirst/Last | O(1) |
| peekFirst/Last | O(1) |
| size | O(1) |
| contains | O(n) |

## 💻 Exemplos Práticos

### Exemplo 1: ArrayDeque como Stack

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class StackComArrayDeque {
    public static void main(String[] args) {
        Deque<Integer> pilha = new ArrayDeque<>();
        
        // Push
        pilha.push(1);
        pilha.push(2);
        pilha.push(3);
        
        // Pop
        System.out.println(pilha.pop()); // 3
        System.out.println(pilha.pop()); // 2
        
        // Peek
        System.out.println(pilha.peek()); // 1
    }
}
```

### Exemplo 2: ArrayDeque como Queue

```java
import java.util.ArrayDeque;
import java.util.Queue;

public class FilaComArrayDeque {
    public static void main(String[] args) {
        Queue<String> fila = new ArrayDeque<>();
        
        fila.offer("Primeiro");
        fila.offer("Segundo");
        fila.offer("Terceiro");
        
        while (!fila.isEmpty()) {
            System.out.println(fila.poll());
        }
        // Output: Primeiro, Segundo, Terceiro
    }
}
```

### Exemplo 3: Sliding Window Maximum

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class SlidingWindowMax {
    public static int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || k <= 0) return new int[0];
        
        int[] result = new int[nums.length - k + 1];
        Deque<Integer> deque = new ArrayDeque<>();
        
        for (int i = 0; i < nums.length; i++) {
            // Remove índices fora da janela
            while (!deque.isEmpty() && deque.peek() < i - k + 1) {
                deque.poll();
            }
            
            // Remove elementos menores que o atual
            while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
                deque.pollLast();
            }
            
            deque.offer(i);
            
            // Adiciona resultado quando janela está completa
            if (i >= k - 1) {
                result[i - k + 1] = nums[deque.peek()];
            }
        }
        
        return result;
    }
    
    public static void main(String[] args) {
        int[] nums = {1, 3, -1, -3, 5, 3, 6, 7};
        int k = 3;
        
        int[] result = maxSlidingWindow(nums, k);
        
        System.out.print("Máximos da janela: ");
        for (int max : result) {
            System.out.print(max + " ");
        }
        // Output: 3 3 5 5 6 7
    }
}
```

## 🎯 Quando Usar

**Use ArrayDeque como preferência para:**
- Implementar Stack (ao invés de Stack class)
- Implementar Queue (ao invés de LinkedList)
- Operações em ambas as pontas
- Quando null não é necessário

## 🔗 Relacionados
- [Deque](./deque.md)
- [LinkedList](./linkedlist.md)
- [Stack](./stack.md)

---

[← Voltar ao Índice](../README.md)
