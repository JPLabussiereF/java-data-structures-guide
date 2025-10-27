# Comparação Geral de Estruturas de Dados

[← Voltar ao Índice](../README.md)

## 📊 Tabela Comparativa Completa

### Estruturas de Lista

| Estrutura | Acesso | Inserção Início | Inserção Final | Busca | Thread-Safe | Permite Null |
|-----------|--------|----------------|----------------|-------|-------------|--------------|
| **Array** | O(1) | O(n) | O(1)* | O(n) | Não | Sim |
| **ArrayList** | O(1) | O(n) | O(1)† | O(n) | Não | Sim |
| **LinkedList** | O(n) | O(1) | O(1) | O(n) | Não | Sim |
| **Vector** | O(1) | O(n) | O(1)† | O(n) | Sim | Sim |

*Se houver espaço pré-alocado  
†Amortizado (pode ser O(n) ao redimensionar)

### Estruturas de Conjunto (Set)

| Estrutura | Add | Remove | Contains | Ordenado | Ordem Inserção | Permite Null | Thread-Safe |
|-----------|-----|--------|----------|----------|----------------|--------------|-------------|
| **HashSet** | O(1) | O(1) | O(1) | Não | Não | Sim (1x) | Não |
| **LinkedHashSet** | O(1) | O(1) | O(1) | Não | Sim | Sim (1x) | Não |
| **TreeSet** | O(log n) | O(log n) | O(log n) | Sim | Não | Não | Não |

### Estruturas de Mapa (Map)

| Estrutura | Get | Put | Remove | Ordenado | Ordem Inserção | Null Key | Null Value | Thread-Safe |
|-----------|-----|-----|--------|----------|----------------|----------|------------|-------------|
| **HashMap** | O(1) | O(1) | O(1) | Não | Não | Sim (1x) | Sim | Não |
| **LinkedHashMap** | O(1) | O(1) | O(1) | Não | Sim | Sim (1x) | Sim | Não |
| **TreeMap** | O(log n) | O(log n) | O(log n) | Sim | Não | Não | Sim | Não |
| **Hashtable** | O(1) | O(1) | O(1) | Não | Não | Não | Não | Sim (lento) |
| **ConcurrentHashMap** | O(1) | O(1) | O(1) | Não | Não | Não | Não | Sim (rápido) |

### Estruturas de Fila

| Estrutura | Offer | Poll | Peek | Ordenado | Thread-Safe | Permite Null |
|-----------|-------|------|------|----------|-------------|--------------|
| **LinkedList** | O(1) | O(1) | O(1) | FIFO | Não | Sim |
| **ArrayDeque** | O(1)† | O(1) | O(1) | FIFO/LIFO | Não | Não |
| **PriorityQueue** | O(log n) | O(log n) | O(1) | Por prioridade | Não | Não |

†Amortizado

### Estruturas de Pilha

| Estrutura | Push | Pop | Peek | Thread-Safe | Permite Null |
|-----------|------|-----|------|-------------|--------------|
| **Stack** (legado) | O(1) | O(1) | O(1) | Sim | Sim |
| **ArrayDeque** | O(1) | O(1) | O(1) | Não | Não |

## 🎯 Uso de Memória

**Mais Eficiente → Menos Eficiente:**

1. **Arrays primitivos** - Sem overhead
2. **ArrayList** - Pequeno overhead + capacidade extra
3. **HashMap/HashSet** - Overhead de buckets + load factor
4. **LinkedList/LinkedHashMap** - Overhead de ponteiros (anterior + próximo)
5. **TreeMap/TreeSet** - Overhead de nós da árvore (left, right, parent, color)

## ⚡ Performance em Casos Comuns

### Acesso Aleatório
🥇 Array / ArrayList: O(1)  
🥈 HashMap (por chave): O(1)  
🥉 LinkedList: O(n) ❌

### Inserção no Início
🥇 LinkedList: O(1)  
🥇 ArrayDeque: O(1)  
🥉 ArrayList: O(n) ❌

### Inserção no Final
🥇 ArrayList (com capacidade): O(1)  
🥇 LinkedList: O(1)  
🥇 ArrayDeque: O(1)

### Busca de Elemento
🥇 HashSet/HashMap: O(1)  
🥈 TreeSet/TreeMap: O(log n)  
🥉 ArrayList/LinkedList: O(n) ❌

### Elementos Ordenados
🥇 TreeSet/TreeMap: Sempre ordenado  
🥈 ArrayList: Precisa chamar Collections.sort() - O(n log n)  
🥉 HashSet/HashMap: Não ordenável ❌

## 🔄 Conversões Comuns

```java
// List → Set (remove duplicatas)
Set<T> set = new HashSet<>(lista);

// Set → List
List<T> lista = new ArrayList<>(conjunto);

// Array → List
List<T> lista = Arrays.asList(array);
List<T> listaMutavel = new ArrayList<>(Arrays.asList(array));

// List → Array
T[] array = lista.toArray(new T[0]);

// Map keys/values → Collection
Set<K> chaves = map.keySet();
Collection<V> valores = map.values();
Set<Map.Entry<K,V>> entradas = map.entrySet();
```

## 📈 Cenários de Uso

| Cenário | Estrutura Recomendada | Por quê? |
|---------|----------------------|----------|
| Cache por chave | HashMap | O(1) lookup |
| Cache com ordem | LinkedHashMap | O(1) + ordem |
| Elementos únicos | HashSet | O(1) + sem duplicatas |
| Elementos únicos ordenados | TreeSet | O(log n) + ordenado |
| Lista de tamanho conhecido | ArrayList com capacidade | Evita redimensionamento |
| Inserções frequentes no início | LinkedList ou ArrayDeque | O(1) |
| Fila FIFO | ArrayDeque | Melhor performance |
| Pilha LIFO | ArrayDeque | Melhor que Stack |
| Fila por prioridade | PriorityQueue | Heap eficiente |
| Multi-thread | ConcurrentHashMap | Alta concorrência |
| LRU Cache | LinkedHashMap (access order) | Remove menos usado |
| Range queries | TreeMap/TreeSet | subSet, headSet, tailSet |
| Top K elementos | PriorityQueue | Heap mantém K elementos |

## 🚨 Erros Comuns

### 1. Usar LinkedList por Padrão
```java
// ❌ Evite (na maioria dos casos)
List<String> lista = new LinkedList<>();

// ✅ Prefira
List<String> lista = new ArrayList<>();
```

### 2. Usar Stack Legado
```java
// ❌ Evite
Stack<Integer> pilha = new Stack<>();

// ✅ Prefira
Deque<Integer> pilha = new ArrayDeque<>();
```

### 3. Não Pré-Alocar Capacidade
```java
// ❌ Ineficiente (redimensiona várias vezes)
List<Integer> lista = new ArrayList<>();
for (int i = 0; i < 100000; i++) lista.add(i);

// ✅ Eficiente
List<Integer> lista = new ArrayList<>(100000);
for (int i = 0; i < 100000; i++) lista.add(i);
```

### 4. Modificar Durante Iteração
```java
// ❌ ConcurrentModificationException
for (String item : lista) {
    if (condicao) lista.remove(item);
}

// ✅ Use Iterator ou removeIf
lista.removeIf(item -> condicao);
```

### 5. Usar Hashtable
```java
// ❌ Legado e lento
Map<K, V> map = new Hashtable<>();

// ✅ Use HashMap ou ConcurrentHashMap
Map<K, V> map = new HashMap<>(); // single-thread
Map<K, V> map = new ConcurrentHashMap<>(); // multi-thread
```

## 💡 Dicas de Otimização

1. **Escolha a estrutura certa primeiro** - Otimização prematura é má, mas estrutura errada é pior

2. **Considere o caso de uso dominante:**
   - Mais leituras → HashMap/HashSet
   - Mais escritas no início → LinkedList/ArrayDeque
   - Ordenação necessária → TreeMap/TreeSet

3. **Pré-aloque quando souber o tamanho:**
   ```java
   new ArrayList<>(tamanhoEsperado)
   new HashMap<>(tamanhoEsperado)
   ```

4. **Use tipos primitivos quando possível:**
   ```java
   int[] array = new int[1000];  // Melhor que
   ArrayList<Integer> lista = new ArrayList<>();  // Boxing overhead
   ```

5. **Considere thread-safety apenas quando necessário** - Tem custo de performance

## 🔗 Guia de Decisão Rápida

```
Precisa de ordem? 
├─ NÃO → Use HashMap/HashSet (mais rápido)
└─ SIM → 
   ├─ Ordem de inserção → LinkedHashMap/LinkedHashSet
   └─ Ordem natural/comparador → TreeMap/TreeSet

Precisa de List?
├─ Acesso por índice frequente → ArrayList
├─ Inserções/remoções no início → ArrayDeque ou LinkedList
└─ Geral → ArrayList (padrão seguro)

Precisa de Queue?
├─ FIFO simples → ArrayDeque
├─ Por prioridade → PriorityQueue
└─ Thread-safe → ConcurrentLinkedQueue

Precisa de Map thread-safe?
└─ ConcurrentHashMap (sempre! Nunca Hashtable)
```

---

[← Voltar ao Índice](../README.md) | [Guia de Seleção →](./guia-selecao.md)
