# ✅ Checklist: Escolhendo a Estrutura de Dados Correta

Use este checklist antes de escolher uma estrutura de dados no seu projeto.

## 📋 Perguntas Essenciais

### 1. Tipo de Dado
- [ ] Preciso armazenar valores únicos? → Consider **Set**
- [ ] Preciso de pares chave-valor? → Consider **Map**
- [ ] Preciso de uma sequência ordenada? → Consider **List**
- [ ] Preciso de processamento FIFO/LIFO? → Consider **Queue/Deque**

### 2. Operações Mais Frequentes

#### Para Listas:
- [ ] Acesso por índice é frequente? → **ArrayList**
- [ ] Inserções no início são frequentes? → **LinkedList** ou **ArrayDeque**
- [ ] Inserções no final são frequentes? → **ArrayList**
- [ ] Inserções/remoções no meio são frequentes? → **LinkedList** (mas reavalie se realmente precisa)

#### Para Sets:
- [ ] Apenas preciso eliminar duplicatas? → **HashSet**
- [ ] Preciso manter ordem de inserção? → **LinkedHashSet**
- [ ] Preciso de elementos ordenados? → **TreeSet**

#### Para Maps:
- [ ] Lookup por chave é a operação principal? → **HashMap**
- [ ] Preciso iterar em ordem de inserção? → **LinkedHashMap**
- [ ] Preciso de chaves ordenadas? → **TreeMap**
- [ ] Preciso de operações range? → **TreeMap**

### 3. Requisitos de Ordenação
- [ ] Elementos devem estar sempre ordenados? → **TreeSet** / **TreeMap**
- [ ] Ordem de inserção deve ser preservada? → **LinkedHashSet** / **LinkedHashMap**
- [ ] Ordem não importa (mais rápido)? → **HashSet** / **HashMap**
- [ ] Posso ordenar depois se necessário? → **ArrayList** + `Collections.sort()`

### 4. Concorrência
- [ ] Múltiplas threads vão acessar simultaneamente? → **ConcurrentHashMap**
- [ ] Preciso de sincronização total? → `Collections.synchronizedXXX()`
- [ ] Apenas uma thread? → Estruturas normais (mais rápidas)

### 5. Elementos Null
- [ ] Preciso armazenar null? 
  - ✅ Permitido: ArrayList, LinkedList, HashMap, HashSet
  - ❌ NÃO permitido: TreeMap, TreeSet, ArrayDeque, ConcurrentHashMap

### 6. Performance Crítica
- [ ] Milhões de elementos? → Considere uso de memória e cache locality
- [ ] Operações devem ser O(1)? → Hash-based (HashMap, HashSet)
- [ ] O(log n) é aceitável para ter ordem? → Tree-based (TreeMap, TreeSet)
- [ ] Trabalhando com primitivos? → Arrays primitivos (evite boxing)

### 7. Tamanho
- [ ] Tamanho é fixo e conhecido? → **Array** primitivo
- [ ] Tamanho é aproximadamente conhecido? → Pré-aloque capacidade
- [ ] Tamanho é completamente dinâmico? → ArrayList / HashMap

### 8. Casos Especiais
- [ ] Implementando cache? → **HashMap** ou **LinkedHashMap** (LRU)
- [ ] Implementando fila de prioridade? → **PriorityQueue**
- [ ] Implementando pilha? → **ArrayDeque** (como Deque)
- [ ] Implementando fila? → **ArrayDeque** (como Queue)
- [ ] Contando frequências? → **HashMap**
- [ ] BFS/DFS? → **ArrayDeque** + **HashSet**
- [ ] Dijkstra/A*? → **PriorityQueue** + **HashMap**
- [ ] Histórico undo/redo? → **ArrayDeque** (2 pilhas)

## 🎯 Decisão Final

Com base nas respostas acima:

### Se você respondeu SIM para:
- "Acesso por índice frequente" → `ArrayList<T>`
- "Lookup por chave" → `HashMap<K, V>`
- "Elementos únicos sem ordem" → `HashSet<T>`
- "Elementos únicos ordenados" → `TreeSet<T>`
- "Pilha" → `Deque<T> pilha = new ArrayDeque<>()`
- "Fila" → `Queue<T> fila = new ArrayDeque<>()`
- "Multi-thread" → `ConcurrentHashMap<K, V>`
- "LRU Cache" → `LinkedHashMap<K, V>` com removeEldestEntry

### Ainda em dúvida?
1. **Para Listas**: Use `ArrayList` (padrão seguro)
2. **Para Mapas**: Use `HashMap` (padrão seguro)
3. **Para Conjuntos**: Use `HashSet` (padrão seguro)
4. **Para Filas/Pilhas**: Use `ArrayDeque` (padrão seguro)

## ⚠️ Sinais de Alerta

### Você pode estar usando a estrutura ERRADA se:
- [ ] Está fazendo `get(i)` em LinkedList
- [ ] Está usando Stack ao invés de ArrayDeque
- [ ] Está usando Hashtable ao invés de HashMap/ConcurrentHashMap
- [ ] ArrayList com muitas inserções no índice 0
- [ ] Não pré-alocou capacidade e conhece o tamanho
- [ ] Iterando com índice em LinkedList: `for(int i=0; i<list.size(); i++)`
- [ ] Usando TreeMap/TreeSet mas ordem não é necessária

## 💡 Otimizações Comuns

### Já escolheu? Considere:
- [ ] Pré-alocar capacidade inicial se souber o tamanho aproximado
- [ ] Usar `ArrayList` com `Collections.sort()` ao invés de TreeSet (se ordenação não é constante)
- [ ] Usar arrays primitivos para grandes volumes de números
- [ ] Trocar TreeSet por HashSet se ordenação não é realmente necessária
- [ ] Considerar se realmente precisa de LinkedList (ArrayList geralmente é melhor)

## 📚 Exemplos de Código Rápido

```java
// Lista geral
List<String> lista = new ArrayList<>();

// Mapa geral  
Map<String, Integer> mapa = new HashMap<>();

// Conjunto único
Set<String> conjunto = new HashSet<>();

// Pilha
Deque<Integer> pilha = new ArrayDeque<>();
pilha.push(1);
int topo = pilha.pop();

// Fila
Queue<String> fila = new ArrayDeque<>();
fila.offer("item");
String primeiro = fila.poll();

// Multi-thread
Map<String, Object> cache = new ConcurrentHashMap<>();

// Heap (prioridade)
PriorityQueue<Integer> heap = new PriorityQueue<>();
```

## 🔗 Próximos Passos

- [ ] Leia a [Referência Rápida](./QUICK_REFERENCE.md)
- [ ] Consulte o [Guia de Seleção](./docs/guia-selecao.md) para casos específicos
- [ ] Veja a [Comparação Completa](./docs/comparacao-geral.md)
- [ ] Leia documentação específica da estrutura escolhida

---

**Lembre-se:** A escolha "perfeita" muitas vezes não importa tanto. Escolha uma boa o suficiente e otimize depois se necessário!
