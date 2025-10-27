# Guia de Seleção: Qual Estrutura Usar?

[← Voltar ao Índice](../README.md)

## 🎯 Árvore de Decisão

Siga o fluxo abaixo para encontrar a estrutura ideal:

```
┌─────────────────────────────────────┐
│ Que tipo de dado você precisa?     │
└──────────────┬──────────────────────┘
               │
       ┌───────┴───────┐
       │               │
   ┌───▼───┐      ┌───▼────┐
   │ ÚNICO │      │ PARES  │
   │(valor)│      │(k → v) │
   └───┬───┘      └───┬────┘
       │              │
       │              │
   [Set]          [Map]
       │              │
       │              └──→ Veja seção MAP abaixo
       │
       └──→ Precisa manter ordem?
            │
            ├─→ NÃO: HashSet
            ├─→ Ordem de inserção: LinkedHashSet  
            └─→ Ordem natural: TreeSet
```

## 📋 LISTA (Sequência de Elementos)

### Pergunta 1: Tamanho é fixo e conhecido?
```
SIM → Array primitivo (int[], String[], etc)
NÃO → Continue...
```

### Pergunta 2: Qual operação é mais frequente?

#### A) **Acesso por índice** (get)
```java
✅ ArrayList
// Acesso O(1), excelente para iteração
List<String> lista = new ArrayList<>();
```

#### B) **Inserção/remoção no INÍCIO**
```java
✅ ArrayDeque ou LinkedList
// Ambos O(1) no início
Deque<String> deque = new ArrayDeque<>();
// ou
LinkedList<String> lista = new LinkedList<>();
```

#### C) **Inserção/remoção no FINAL**
```java
✅ ArrayList
// O(1) amortizado, melhor cache locality
List<String> lista = new ArrayList<>();
```

#### D) **Inserção/remoção no MEIO (frequente)**
```java
✅ LinkedList
// O(1) após localização, mas considere se realmente precisa
LinkedList<String> lista = new LinkedList<>();
```

### Caso Especial: Precisa de pilha ou fila?

```java
// PILHA (LIFO) - use ArrayDeque
Deque<String> pilha = new ArrayDeque<>();
pilha.push("item");
String topo = pilha.pop();

// FILA (FIFO) - use ArrayDeque
Queue<String> fila = new ArrayDeque<>();
fila.offer("item");
String primeiro = fila.poll();
```

## 🔑 MAP (Chave → Valor)

### Pergunta 1: Precisa de thread-safety?
```
SIM → ConcurrentHashMap
NÃO → Continue...
```

### Pergunta 2: Precisa de ordem?

#### A) **NÃO precisa de ordem**
```java
✅ HashMap
// Mais rápido, caso padrão
Map<String, Integer> map = new HashMap<>();
```

#### B) **Ordem de INSERÇÃO**
```java
✅ LinkedHashMap
// Mantém ordem de inserção
Map<String, Integer> map = new LinkedHashMap<>();

// Para LRU cache:
Map<K, V> lru = new LinkedHashMap<>(capacity, 0.75f, true) {
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > capacity;
    }
};
```

#### C) **Ordem NATURAL** (alfabética/numérica)
```java
✅ TreeMap
// Chaves sempre ordenadas
Map<String, Integer> map = new TreeMap<>();

// Ou com comparador customizado:
Map<String, Integer> map = new TreeMap<>(Collections.reverseOrder());
```

## 🎨 SET (Elementos Únicos)

### Árvore de Decisão

```
Precisa de ordem?
│
├─→ NÃO → HashSet
│   └─→ Verificação O(1), mais rápido
│
├─→ Ordem de INSERÇÃO → LinkedHashSet  
│   └─→ Remove duplicatas MAS mantém ordem
│
└─→ Ordem NATURAL → TreeSet
    └─→ Sempre ordenado, operações O(log n)
```

### Exemplos de Código

```java
// 1. SEM ordem - mais comum e rápido
Set<String> visitados = new HashSet<>();
visitados.add("site1");
if (visitados.contains("site1")) { ... } // O(1)

// 2. COM ordem de inserção
Set<String> tags = new LinkedHashSet<>();
tags.add("java");
tags.add("python");
tags.add("java"); // ignorado
// Iteração: java, python (nessa ordem)

// 3. ORDENADO naturalmente
Set<Integer> numeros = new TreeSet<>();
numeros.add(5);
numeros.add(1);
numeros.add(3);
// Iteração: 1, 3, 5 (sempre ordenado)
```

## 🚀 QUEUE (Fila)

### Qual tipo de fila?

#### A) **FIFO Simples** (primeiro a entrar, primeiro a sair)
```java
✅ ArrayDeque
// Implementação mais eficiente
Queue<Task> fila = new ArrayDeque<>();
fila.offer(task);
Task next = fila.poll();
```

#### B) **Por PRIORIDADE** (menor/maior primeiro)
```java
✅ PriorityQueue
// Min-heap por padrão
Queue<Integer> heap = new PriorityQueue<>();

// Max-heap (reverso)
Queue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

// Com comparador customizado
Queue<Task> tasks = new PriorityQueue<>(
    Comparator.comparingInt(Task::getPriority)
);
```

#### C) **Dupla** (opera em ambas as pontas)
```java
✅ ArrayDeque
Deque<String> deque = new ArrayDeque<>();
deque.addFirst("início");
deque.addLast("fim");
deque.removeFirst();
deque.removeLast();
```

## 🏗️ STACK (Pilha - LIFO)

```java
// ❌ NUNCA use Stack (legado)
Stack<Integer> pilha = new Stack<>();  // NÃO!

// ✅ SEMPRE use ArrayDeque
Deque<Integer> pilha = new ArrayDeque<>();
pilha.push(1);
pilha.push(2);
int topo = pilha.pop(); // 2
```

## 🎪 Casos de Uso Específicos

### Cache de Objetos
```java
// Cache simples
Map<String, Object> cache = new HashMap<>();

// LRU Cache (remove menos usado)
Map<String, Object> lruCache = new LinkedHashMap<>(16, 0.75f, true) {
    protected boolean removeEldestEntry(Map.Entry eldest) {
        return size() > MAX_ENTRIES;
    }
};

// Cache thread-safe
Map<String, Object> cache = new ConcurrentHashMap<>();
```

### Eliminar Duplicatas
```java
// Simples e rápido
List<T> semDuplicatas = new ArrayList<>(new HashSet<>(listaOriginal));

// Mantendo ordem original
List<T> semDuplicatas = new ArrayList<>(new LinkedHashSet<>(listaOriginal));
```

### Top K Elementos
```java
// Use PriorityQueue (heap)
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
for (int num : array) {
    minHeap.offer(num);
    if (minHeap.size() > k) {
        minHeap.poll();
    }
}
// minHeap contém os K maiores
```

### Contador de Frequência
```java
Map<String, Integer> frequencia = new HashMap<>();
for (String palavra : palavras) {
    frequencia.merge(palavra, 1, Integer::sum);
}
```

### Histórico de Ações (Undo/Redo)
```java
Deque<Action> undoStack = new ArrayDeque<>();
Deque<Action> redoStack = new ArrayDeque<>();

void executarAcao(Action acao) {
    undoStack.push(acao);
    redoStack.clear();
}

void undo() {
    if (!undoStack.isEmpty()) {
        Action acao = undoStack.pop();
        redoStack.push(acao);
        acao.reverter();
    }
}

void redo() {
    if (!redoStack.isEmpty()) {
        Action acao = redoStack.pop();
        undoStack.push(acao);
        acao.executar();
    }
}
```

### BFS (Busca em Largura)
```java
Queue<Node> fila = new ArrayDeque<>();
Set<Node> visitados = new HashSet<>();

fila.offer(inicio);
visitados.add(inicio);

while (!fila.isEmpty()) {
    Node atual = fila.poll();
    for (Node vizinho : atual.getVizinhos()) {
        if (!visitados.contains(vizinho)) {
            visitados.add(vizinho);
            fila.offer(vizinho);
        }
    }
}
```

### DFS (Busca em Profundidade)
```java
Deque<Node> pilha = new ArrayDeque<>();
Set<Node> visitados = new HashSet<>();

pilha.push(inicio);

while (!pilha.isEmpty()) {
    Node atual = pilha.pop();
    if (!visitados.contains(atual)) {
        visitados.add(atual);
        for (Node vizinho : atual.getVizinhos()) {
            pilha.push(vizinho);
        }
    }
}
```

### Dijkstra / A* (Menor Caminho)
```java
PriorityQueue<Node> pq = new PriorityQueue<>(
    Comparator.comparingInt(Node::getDistancia)
);
Map<Node, Integer> distancias = new HashMap<>();

pq.offer(inicio);
distancias.put(inicio, 0);

while (!pq.isEmpty()) {
    Node atual = pq.poll();
    // processar vizinhos...
}
```

## ⚡ Regras de Ouro

### 1. **Na dúvida, use ArrayList**
É rápido para 90% dos casos e você pode otimizar depois se necessário.

### 2. **HashMap é o Map padrão**
Use HashMap a menos que precise de ordem ou thread-safety.

### 3. **HashSet para unicidade**
Remover duplicatas ou verificar existência rapidamente.

### 4. **ArrayDeque para pilhas e filas**
Mais rápido que Stack e LinkedList.

### 5. **TreeMap/TreeSet apenas quando precisa de ordem**
São O(log n), use só se realmente precisa de ordenação.

### 6. **ConcurrentHashMap para multi-thread**
NUNCA use Hashtable.

### 7. **PriorityQueue para heaps**
Top K, menor caminho, scheduling.

## 🚫 O Que EVITAR

```java
// ❌ Stack (use ArrayDeque)
Stack<T> pilha = new Stack<>();

// ❌ Hashtable (use HashMap ou ConcurrentHashMap)
Hashtable<K, V> mapa = new Hashtable<>();

// ❌ Vector (use ArrayList)
Vector<T> vetor = new Vector<>();

// ❌ LinkedList para acesso aleatório
LinkedList<T> lista = new LinkedList<>();
for (int i = 0; i < lista.size(); i++) {
    lista.get(i); // O(n) a cada chamada! LENTO
}

// ❌ ArrayList para muitas inserções no início
ArrayList<T> lista = new ArrayList<>();
for (T item : items) {
    lista.add(0, item); // O(n) - muito lento!
}
```

## 📊 Checklist de Seleção

Ao escolher uma estrutura, pergunte-se:

- [ ] Qual operação será mais frequente?
- [ ] Preciso de ordem? Qual tipo?
- [ ] Preciso de thread-safety?
- [ ] Elementos podem ser duplicados?
- [ ] Qual o tamanho esperado?
- [ ] Acesso será aleatório ou sequencial?
- [ ] Null é permitido/necessário?
- [ ] Performance é crítica?

## 🔗 Referência Rápida

| Preciso de... | Use |
|--------------|-----|
| Lista geral | `ArrayList` |
| Pilha | `ArrayDeque` (como Deque) |
| Fila FIFO | `ArrayDeque` (como Queue) |
| Fila de prioridade | `PriorityQueue` |
| Mapa rápido | `HashMap` |
| Mapa ordenado | `TreeMap` |
| Mapa com ordem de inserção | `LinkedHashMap` |
| Conjunto único | `HashSet` |
| Conjunto ordenado | `TreeSet` |
| Thread-safe map | `ConcurrentHashMap` |
| LRU Cache | `LinkedHashMap` (access-order) |

---

[← Voltar ao Índice](../README.md) | [Ver Comparação Completa](./comparacao-geral.md)
