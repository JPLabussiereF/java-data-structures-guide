# 🚀 Referência Rápida - Estruturas de Dados Java

## ⚡ Escolha em 30 Segundos

```
PRECISO DE UMA LISTA
├─ Acesso por índice frequente? → ArrayList
├─ Inserções no início? → ArrayDeque ou LinkedList  
└─ Uso geral? → ArrayList (padrão seguro)

PRECISO ELIMINAR DUPLICATAS
├─ Sem ordem? → HashSet (mais rápido)
├─ Manter ordem de inserção? → LinkedHashSet
└─ Ordem alfabética/numérica? → TreeSet

PRECISO DE CHAVE → VALOR
├─ Multi-thread? → ConcurrentHashMap
├─ Ordem alfabética/numérica? → TreeMap
├─ Manter ordem de inserção? → LinkedHashMap
└─ Uso geral? → HashMap (padrão seguro)

PRECISO DE FILA/PILHA
├─ Pilha (LIFO)? → ArrayDeque (como Deque)
├─ Fila simples (FIFO)? → ArrayDeque (como Queue)
└─ Fila por prioridade? → PriorityQueue
```

## 📊 Complexidade em Uma Tabela

| Estrutura | Acesso | Inserção | Busca | Ordenado? | Thread-Safe? |
|-----------|--------|----------|-------|-----------|--------------|
| **ArrayList** | O(1) | O(1)* final<br>O(n) início | O(n) | ❌ | ❌ |
| **LinkedList** | O(n) | O(1) pontas<br>O(n) meio | O(n) | ❌ | ❌ |
| **HashSet** | - | O(1) | O(1) | ❌ | ❌ |
| **TreeSet** | - | O(log n) | O(log n) | ✅ | ❌ |
| **HashMap** | O(1) | O(1) | O(1) | ❌ | ❌ |
| **TreeMap** | O(log n) | O(log n) | O(log n) | ✅ | ❌ |
| **ArrayDeque** | O(n) | O(1) pontas | O(n) | ❌ | ❌ |
| **PriorityQueue** | O(1)† | O(log n) | O(n) | ✅‡ | ❌ |
| **ConcurrentHashMap** | O(1) | O(1) | O(1) | ❌ | ✅ |

*Amortizado  
†Apenas peek (topo do heap)  
‡Por prioridade, não ordenação total

## 🎯 Casos de Uso Comuns

| Eu quero... | Use isto |
|------------|----------|
| Guardar usuários únicos | `Set<User> usuarios = new HashSet<>()` |
| Cache rápido por ID | `Map<Long, User> cache = new HashMap<>()` |
| Fila de tarefas | `Queue<Task> fila = new ArrayDeque<>()` |
| Histórico de undo | `Deque<Action> undo = new ArrayDeque<>()` |
| Top 10 scores | `PriorityQueue<Score> top = new PriorityQueue<>()` |
| Contagem de palavras | `Map<String, Integer> freq = new HashMap<>()` |
| Lista ordenada | `List<String> nomes = new ArrayList<>();`<br>`Collections.sort(nomes)` |
| Elementos únicos ordenados | `Set<Integer> nums = new TreeSet<>()` |
| LRU Cache | `LinkedHashMap` com `removeEldestEntry` |
| Config thread-safe | `Map<String, String> config = new ConcurrentHashMap<>()` |

## ⚠️ Erros Comuns - EVITE!

```java
// ❌ NUNCA faça isso:
Stack<Integer> pilha = new Stack<>();          // Legado - use ArrayDeque
Hashtable<K,V> map = new Hashtable<>();        // Legado - use HashMap/ConcurrentHashMap
Vector<String> lista = new Vector<>();         // Legado - use ArrayList

// ❌ LENTO:
LinkedList<T> lista = new LinkedList<>();
for (int i = 0; i < lista.size(); i++) {
    lista.get(i); // O(n²) total!
}

// ✅ CORRETO:
for (T item : lista) {  // O(n) com iterator
    // processar item
}
```

## 💡 Dicas de Performance

1. **Pré-aloque quando souber o tamanho:**
   ```java
   new ArrayList<>(1000)
   new HashMap<>(1000)
   ```

2. **ArrayList > LinkedList** na maioria dos casos

3. **HashMap > TreeMap** se não precisa de ordem

4. **HashSet.contains() é O(1)**, List.contains() é O(n)

5. **ArrayDeque > LinkedList** para pilhas e filas

## 🔗 Links Rápidos

- [Comparação Completa](docs/comparacao-geral.md)
- [Guia de Seleção Detalhado](docs/guia-selecao.md)
- [ArrayList vs Array](docs/arrays-arraylist.md)
- [HashMap](docs/hashmap.md)
- [TreeMap e TreeSet](docs/treemap.md)

---

**Dica Final:** Na dúvida, comece com ArrayList (lista) ou HashMap (mapa). Você pode otimizar depois se necessário!
