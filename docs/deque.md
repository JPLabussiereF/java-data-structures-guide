# Deque (Double-Ended Queue)

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

Deque (pronuncia-se "deck") é uma fila de duas pontas que permite inserção e remoção eficiente em ambas as extremidades.

## 🔍 Implementações

- **ArrayDeque**: Array circular (RECOMENDADA)
- **LinkedList**: Lista duplamente encadeada

## ⚖️ Trade-offs

### ✅ Vantagens
- Operações O(1) em ambas as pontas
- Substitui Stack e Queue com melhor performance
- ArrayDeque é cache-friendly
- Versátil (pilha, fila, fila dupla)

### ❌ Desvantagens  
- Sem acesso aleatório eficiente
- ArrayDeque não permite null
- Maior complexidade conceitual

## 📊 Complexidade

| Operação | ArrayDeque | LinkedList |
|----------|-----------|------------|
| addFirst/Last | O(1) | O(1) |
| removeFirst/Last | O(1) | O(1) |
| getFirst/Last | O(1) | O(1) |
| Acesso por índice | O(n) | O(n) |

## 💻 Exemplos

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class DequeExemplo {
    public static void main(String[] args) {
        Deque<String> deque = new ArrayDeque<>();
        
        // Operações no início
        deque.addFirst("A");
        deque.addFirst("B");
        
        // Operações no final
        deque.addLast("C");
        deque.addLast("D");
        
        // Resultado: B A C D
        System.out.println(deque);
        
        // Remove das duas pontas
        deque.removeFirst(); // Remove B
        deque.removeLast();  // Remove D
        
        // Resultado: A C
        System.out.println(deque);
    }
}
```

## 🔗 Relacionados
- [ArrayDeque](./arraydeque.md)
- [LinkedList](./linkedlist.md)
- [Stack](./stack.md)
- [Queue](./queue.md)

---

[← Voltar ao Índice](../README.md)
