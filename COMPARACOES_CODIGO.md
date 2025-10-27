# 🔬 Comparações de Código: Lado a Lado

Este documento mostra comparações práticas de código para ajudar você a ver as diferenças entre estruturas similares.

## 📋 ArrayList vs LinkedList vs ArrayDeque

### Cenário 1: Adição no Início

```java
// ArrayList - O(n) - LENTO para início
List<String> arrayList = new ArrayList<>();
arrayList.add(0, "novo"); // Desloca todos elementos

// LinkedList - O(1) - RÁPIDO para início  
LinkedList<String> linkedList = new LinkedList<>();
linkedList.addFirst("novo"); // Apenas ajusta ponteiros

// ArrayDeque - O(1) - RÁPIDO para início
Deque<String> arrayDeque = new ArrayDeque<>();
arrayDeque.addFirst("novo"); // Ajusta índice circular
```

### Cenário 2: Acesso por Índice

```java
// ArrayList - O(1) - RÁPIDO ✅
arrayList.get(100); // Acesso direto ao array

// LinkedList - O(n) - LENTO ❌
linkedList.get(100); // Percorre 100 nós!

// ArrayDeque - O(n) - LENTO ❌
// (Não é feito para acesso aleatório)
```

### Cenário 3: Iteração Completa

```java
// ArrayList - RÁPIDO (cache-friendly)
for (String s : arrayList) { 
    process(s); 
}

// LinkedList - MÉDIO (cache misses)
for (String s : linkedList) { 
    process(s); 
}

// ArrayDeque - RÁPIDO (cache-friendly)
for (String s : arrayDeque) { 
    process(s); 
}
```

**Vencedor Geral:** ArrayList (maioria dos casos)

---

## 🗂️ HashMap vs TreeMap vs LinkedHashMap

### Cenário 1: Put e Get

```java
// HashMap - O(1) - MAIS RÁPIDO ⚡
Map<String, Integer> hashMap = new HashMap<>();
hashMap.put("alice", 30);  // O(1)
hashMap.get("alice");       // O(1)

// TreeMap - O(log n) - MÉDIO
Map<String, Integer> treeMap = new TreeMap<>();
treeMap.put("alice", 30);   // O(log n)
treeMap.get("alice");        // O(log n)

// LinkedHashMap - O(1) - RÁPIDO ⚡
Map<String, Integer> linkedMap = new LinkedHashMap<>();
linkedMap.put("alice", 30);  // O(1)
linkedMap.get("alice");       // O(1)
```

### Cenário 2: Iteração

```java
// HashMap - Ordem IMPREVISÍVEL
hashMap.put("c", 3);
hashMap.put("a", 1);
hashMap.put("b", 2);
for (String key : hashMap.keySet()) {
    System.out.println(key); // Pode ser: b, a, c (aleatório)
}

// TreeMap - Ordem ALFABÉTICA
treeMap.put("c", 3);
treeMap.put("a", 1);
treeMap.put("b", 2);
for (String key : treeMap.keySet()) {
    System.out.println(key); // Sempre: a, b, c
}

// LinkedHashMap - Ordem de INSERÇÃO
linkedMap.put("c", 3);
linkedMap.put("a", 1);
linkedMap.put("b", 2);
for (String key : linkedMap.keySet()) {
    System.out.println(key); // Sempre: c, a, b
}
```

### Cenário 3: Range Queries

```java
// HashMap - NÃO suporta ❌
// (sem métodos de range)

// TreeMap - SUPORTA ✅
TreeMap<String, Integer> tree = new TreeMap<>();
tree.put("alice", 30);
tree.put("bob", 25);
tree.put("charlie", 35);
tree.put("diana", 28);

// Todos entre "bob" e "diana" (exclusivo)
tree.subMap("bob", "diana"); // {bob=25, charlie=35}

// Menores que "charlie"
tree.headMap("charlie"); // {alice=30, bob=25}

// Maiores ou iguais a "bob"
tree.tailMap("bob"); // {bob=25, charlie=35, diana=28}

// LinkedHashMap - NÃO suporta ❌
```

**Escolha:**
- Performance pura? → **HashMap**
- Ordem alfabética/numérica? → **TreeMap**
- Ordem de inserção? → **LinkedHashMap**

---

## 🎯 HashSet vs TreeSet vs LinkedHashSet

### Operações Básicas

```java
// HashSet - Mais rápido, sem ordem
Set<Integer> hashSet = new HashSet<>();
hashSet.add(5);
hashSet.add(1);
hashSet.add(3);
System.out.println(hashSet); // [1, 3, 5] ou [5, 1, 3] - aleatório!

// TreeSet - Ordenado, mais lento
Set<Integer> treeSet = new TreeSet<>();
treeSet.add(5);
treeSet.add(1);
treeSet.add(3);
System.out.println(treeSet); // [1, 3, 5] - sempre ordenado!

// LinkedHashSet - Ordem de inserção
Set<Integer> linkedSet = new LinkedHashSet<>();
linkedSet.add(5);
linkedSet.add(1);
linkedSet.add(3);
System.out.println(linkedSet); // [5, 1, 3] - ordem de inserção!
```

### TreeSet - Funcionalidades Extras

```java
TreeSet<Integer> tree = new TreeSet<>(Arrays.asList(1, 3, 5, 7, 9));

// Menor e maior
tree.first();  // 1
tree.last();   // 9

// Floor e Ceiling
tree.floor(4);    // 3 (maior elemento <= 4)
tree.ceiling(4);  // 5 (menor elemento >= 4)

// Lower e Higher
tree.lower(5);    // 3 (maior elemento < 5)
tree.higher(5);   // 7 (menor elemento > 5)

// Subsets
tree.headSet(5);  // [1, 3] elementos < 5
tree.tailSet(5);  // [5, 7, 9] elementos >= 5
tree.subSet(3, 7); // [3, 5] elementos >= 3 e < 7
```

---

## 📥 ArrayDeque vs LinkedList vs PriorityQueue

### Como Fila (FIFO)

```java
// ArrayDeque - RECOMENDADO ✅
Queue<String> arrayDequeQueue = new ArrayDeque<>();
arrayDequeQueue.offer("primeiro");
arrayDequeQueue.offer("segundo");
arrayDequeQueue.poll(); // "primeiro" - O(1)

// LinkedList - ALTERNATIVA
Queue<String> linkedQueue = new LinkedList<>();
linkedQueue.offer("primeiro");
linkedQueue.offer("segundo");
linkedQueue.poll(); // "primeiro" - O(1)

// Vencedor: ArrayDeque (melhor performance)
```

### Como Pilha (LIFO)

```java
// ArrayDeque - RECOMENDADO ✅
Deque<String> stack = new ArrayDeque<>();
stack.push("primeiro");
stack.push("segundo");
stack.pop(); // "segundo" - O(1)

// LinkedList - ALTERNATIVA
Deque<String> linkedStack = new LinkedList<>();
linkedStack.push("primeiro");
linkedStack.push("segundo");
linkedStack.pop(); // "segundo" - O(1)

// Stack (NÃO USE) ❌
Stack<String> oldStack = new Stack<>();
// Legado, thread-safe desnecessariamente, lento
```

### Fila de Prioridade

```java
// PriorityQueue - Min-heap por padrão
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
minHeap.offer(5);
minHeap.offer(1);
minHeap.offer(3);
minHeap.poll(); // 1 (menor)
minHeap.poll(); // 3
minHeap.poll(); // 5

// PriorityQueue - Max-heap (reverso)
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
maxHeap.offer(5);
maxHeap.offer(1);
maxHeap.offer(3);
maxHeap.poll(); // 5 (maior)
maxHeap.poll(); // 3
maxHeap.poll(); // 1

// ArrayDeque/LinkedList - NÃO tem prioridade
// (saem na ordem FIFO, não por valor)
```

---

## 🔄 HashMap vs ConcurrentHashMap vs Hashtable

### Single-threaded

```java
// HashMap - MAIS RÁPIDO (single-thread) ✅
Map<String, Integer> map = new HashMap<>();
map.put("key", 1);
// Nenhum overhead de sincronização
```

### Multi-threaded

```java
// ConcurrentHashMap - RECOMENDADO para multi-thread ✅
Map<String, Integer> concurrent = new ConcurrentHashMap<>();
// Thread-safe, alta concorrência, rápido

// Operações atômicas
concurrent.putIfAbsent("key", 1);
concurrent.computeIfAbsent("key", k -> expensiveComputation());

// Hashtable - LEGADO (NÃO USE) ❌
Hashtable<String, Integer> old = new Hashtable<>();
// Thread-safe mas LENTO (lock global)

// Collections.synchronizedMap - Alternativa simples
Map<String, Integer> syncMap = Collections.synchronizedMap(new HashMap<>());
// Thread-safe mas menos eficiente que ConcurrentHashMap
```

### Comparação de Performance

```java
// Cenário: 10 threads fazendo 1000 puts cada

// HashMap - FALHA (race conditions) ❌
// Resultado inconsistente, possível perda de dados

// ConcurrentHashMap - RÁPIDO e CORRETO ✅
// ~100ms, sem race conditions

// Hashtable - LENTO mas CORRETO
// ~300ms, lock global causa contenção

// Vencedor: ConcurrentHashMap (multi-thread)
```

---

## 🎯 Casos de Uso: Código Lado a Lado

### Caso 1: Contagem de Frequência

```java
String[] palavras = {"java", "python", "java", "c++", "python", "java"};

// Com HashMap
Map<String, Integer> freq = new HashMap<>();
for (String palavra : palavras) {
    freq.put(palavra, freq.getOrDefault(palavra, 0) + 1);
}

// Ou com merge (mais elegante)
Map<String, Integer> freq2 = new HashMap<>();
for (String palavra : palavras) {
    freq2.merge(palavra, 1, Integer::sum);
}

System.out.println(freq); // {java=3, python=2, c++=1}
```

### Caso 2: Cache LRU

```java
// Com LinkedHashMap (ordem de acesso)
class LRUCache<K, V> extends LinkedHashMap<K, V> {
    private final int capacity;
    
    LRUCache(int capacity) {
        super(capacity, 0.75f, true); // true = access-order
        this.capacity = capacity;
    }
    
    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > capacity;
    }
}

LRUCache<Integer, String> cache = new LRUCache<>(3);
cache.put(1, "A");
cache.put(2, "B");
cache.put(3, "C");
cache.get(1); // Acessa A (move para final)
cache.put(4, "D"); // Remove B (menos usado)
System.out.println(cache); // {3=C, 1=A, 4=D}
```

### Caso 3: Top K Elementos

```java
int[] nums = {1, 1, 1, 2, 2, 3};
int k = 2;

// Com PriorityQueue (min-heap)
PriorityQueue<Integer> heap = new PriorityQueue<>(
    Comparator.comparingInt(n -> frequencia.get(n))
);

Map<Integer, Integer> frequencia = new HashMap<>();
for (int num : nums) {
    frequencia.merge(num, 1, Integer::sum);
}

for (int num : frequencia.keySet()) {
    heap.offer(num);
    if (heap.size() > k) {
        heap.poll(); // Remove o de menor frequência
    }
}

List<Integer> topK = new ArrayList<>(heap);
System.out.println(topK); // [1, 2] (mais frequentes)
```

### Caso 4: Remover Duplicatas Mantendo Ordem

```java
List<Integer> numeros = Arrays.asList(3, 1, 4, 1, 5, 9, 2, 6, 5);

// Com LinkedHashSet (mantém ordem de inserção)
List<Integer> unicos = new ArrayList<>(new LinkedHashSet<>(numeros));
System.out.println(unicos); // [3, 1, 4, 5, 9, 2, 6]

// Com HashSet (ordem aleatória)
List<Integer> unicosDesordenados = new ArrayList<>(new HashSet<>(numeros));
System.out.println(unicosDesordenados); // Ordem imprevisível
```

---

## 💡 Resumo das Comparações

| Cenário | Vencedor | Por quê |
|---------|----------|---------|
| Lista geral | ArrayList | O(1) acesso, cache-friendly |
| Inserções no início | ArrayDeque | O(1) sem overhead de ponteiros |
| Pilha | ArrayDeque | Mais rápido que LinkedList e Stack |
| Fila simples | ArrayDeque | Mais rápido que LinkedList |
| Fila de prioridade | PriorityQueue | Heap eficiente |
| Mapa geral | HashMap | O(1) operações, mais rápido |
| Mapa ordenado | TreeMap | Sempre ordenado |
| Mapa com ordem de inserção | LinkedHashMap | Previsível |
| Set geral | HashSet | O(1) operações, mais rápido |
| Set ordenado | TreeSet | Sempre ordenado |
| Multi-thread | ConcurrentHashMap | Alta concorrência |

---

**Lembre-se:** Benchmarks são úteis, mas escolha baseada no seu caso de uso específico!
