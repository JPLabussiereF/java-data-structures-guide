<div align="center">

# 📚 Guia Completo de Estruturas de Dados em Java

[![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)](https://www.java.com)
[![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)](https://www.markdownguide.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)

*Um guia abrangente sobre estruturas de dados em Java, com análise detalhada de trade-offs, complexidades e exemplos práticos.*

[🚀 Início Rápido](#-início-rápido) •
[📖 Documentação](#-documentação-completa) •
[🎯 Exemplos](#-exemplos) •
[🤝 Contribuir](#-contribuindo)

</div>

---

## 🌟 Destaques

- ✅ **21 documentos completos** cobrindo todas as estruturas principais
- 📊 **Análise de complexidade** (Big O) para cada operação
- ⚖️ **Trade-offs detalhados** com prós e contras
- 💻 **50+ exemplos práticos** comentados
- 🎯 **Guias de decisão** interativos
- 🔬 **Comparações lado a lado** de estruturas similares

## 🚀 Início Rápido

### Para Iniciantes

1. **Leia a [Referência Rápida](./QUICK_REFERENCE.md)** - Decisão em 30 segundos
2. **Use o [Checklist](./CHECKLIST.md)** - Perguntas para te guiar
3. **Consulte os exemplos** - Código prático e funcional

### Para Desenvolvedores Experientes

- **[Comparação Geral](./docs/comparacao-geral.md)** - Tabelas comparativas completas
- **[Comparações de Código](./COMPARACOES_CODIGO.md)** - Benchmarks e exemplos lado a lado
- **Documentação específica** - Mergulhe fundo em cada estrutura

## 📖 Documentação Completa

### 🗂️ Estruturas de Lista

| Estrutura | Acesso | Inserção | Uso Principal | Documentação |
|-----------|--------|----------|---------------|--------------|
| **Array / ArrayList** | O(1) | O(1)* | Lista geral | [📄 Docs](./docs/arrays-arraylist.md) |
| **LinkedList** | O(n) | O(1)† | Inserções nas pontas | [📄 Docs](./docs/linkedlist.md) |

*Amortizado no final | †Nas pontas

### 🎯 Estruturas de Conjunto

| Estrutura | Operações | Ordenado | Documentação |
|-----------|-----------|----------|--------------|
| **HashSet** | O(1) | ❌ | [📄 Docs](./docs/hashset.md) |
| **LinkedHashSet** | O(1) | Inserção | [📄 Docs](./docs/linkedhashset.md) |
| **TreeSet** | O(log n) | ✅ | [📄 Docs](./docs/treeset.md) |

### 🗃️ Estruturas de Mapa

| Estrutura | Operações | Ordenado | Thread-Safe | Documentação |
|-----------|-----------|----------|-------------|--------------|
| **HashMap** | O(1) | ❌ | ❌ | [📄 Docs](./docs/hashmap.md) |
| **LinkedHashMap** | O(1) | Inserção | ❌ | [📄 Docs](./docs/linkedhashmap.md) |
| **TreeMap** | O(log n) | ✅ | ❌ | [📄 Docs](./docs/treemap.md) |
| **ConcurrentHashMap** | O(1) | ❌ | ✅ | [📄 Docs](./docs/concurrenthashmap.md) |

### 📥 Estruturas de Fila/Pilha

| Estrutura | Tipo | Operações | Documentação |
|-----------|------|-----------|--------------|
| **ArrayDeque** | Fila/Pilha | O(1) | [📄 Docs](./docs/arraydeque.md) |
| **PriorityQueue** | Heap | O(log n) | [📄 Docs](./docs/priorityqueue.md) |
| **Stack** | Pilha (⚠️ legado) | O(1) | [📄 Docs](./docs/stack.md) |

## 🎯 Exemplos

### Exemplo: Eliminando Duplicatas

```java
// Mantendo ordem original
List<Integer> original = Arrays.asList(3, 1, 4, 1, 5, 9, 2, 6, 5);
List<Integer> semDuplicatas = new ArrayList<>(new LinkedHashSet<>(original));
// Resultado: [3, 1, 4, 5, 9, 2, 6]
```

### Exemplo: Cache LRU

```java
class LRUCache<K, V> extends LinkedHashMap<K, V> {
    private final int capacity;
    
    LRUCache(int capacity) {
        super(capacity, 0.75f, true); // access-order
        this.capacity = capacity;
    }
    
    @Override
    protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
        return size() > capacity;
    }
}
```

### Exemplo: Top K Elementos

```java
PriorityQueue<Integer> heap = new PriorityQueue<>();
for (int num : array) {
    heap.offer(num);
    if (heap.size() > k) heap.poll();
}
// heap contém os K maiores elementos
```

[**Ver mais exemplos →**](./COMPARACOES_CODIGO.md)

## 🗺️ Guia de Decisão Rápida

```
Preciso de uma LISTA?
├─ Acesso por índice frequente? → ArrayList ⭐
├─ Inserções no início frequentes? → ArrayDeque
└─ Uso geral? → ArrayList (padrão seguro)

Preciso de CHAVE → VALOR?
├─ Multi-thread? → ConcurrentHashMap
├─ Ordenado? → TreeMap
├─ Ordem de inserção? → LinkedHashMap
└─ Uso geral? → HashMap ⭐ (padrão seguro)

Preciso ELIMINAR DUPLICATAS?
├─ Sem ordem? → HashSet ⭐ (mais rápido)
├─ Manter ordem? → LinkedHashSet
└─ Ordenado? → TreeSet

Preciso de FILA/PILHA?
├─ Pilha (LIFO)? → ArrayDeque ⭐
├─ Fila (FIFO)? → ArrayDeque ⭐
└─ Por prioridade? → PriorityQueue
```

## 📚 Índice Completo

### 📘 Guias de Referência
- [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) - Referência rápida com decisão em 30s
- [CHECKLIST.md](./CHECKLIST.md) - Checklist interativo para escolha
- [COMPARACOES_CODIGO.md](./COMPARACOES_CODIGO.md) - Comparações lado a lado

### 📗 Guias Detalhados
- [Guia de Seleção](./docs/guia-selecao.md) - Árvore de decisão completa
- [Comparação Geral](./docs/comparacao-geral.md) - Tabelas comparativas

### 📕 Documentação de Estruturas

**Listas:**
- [Arrays e ArrayList](./docs/arrays-arraylist.md)
- [LinkedList](./docs/linkedlist.md)

**Sets:**
- [HashSet](./docs/hashset.md)
- [LinkedHashSet](./docs/linkedhashset.md)
- [TreeSet](./docs/treeset.md)

**Maps:**
- [HashMap](./docs/hashmap.md)
- [LinkedHashMap](./docs/linkedhashmap.md)
- [TreeMap](./docs/treemap.md)
- [Hashtable](./docs/hashtable.md) ⚠️
- [ConcurrentHashMap](./docs/concurrenthashmap.md)

**Queues & Stacks:**
- [Queue](./docs/queue.md)
- [Deque](./docs/deque.md)
- [ArrayDeque](./docs/arraydeque.md)
- [Stack](./docs/stack.md) ⚠️
- [PriorityQueue](./docs/priorityqueue.md)

## 🎓 Regras de Ouro

1. 🥇 **Na dúvida, use ArrayList** (para listas)
2. 🥇 **Na dúvida, use HashMap** (para mapas)
3. ⚡ **ArrayDeque > LinkedList** (para pilhas e filas)
4. ⚡ **HashSet > TreeSet** (se não precisa de ordem)
5. ⚠️ **NUNCA use**: Stack, Hashtable, Vector (legados)

## 🤝 Contribuindo

Contribuições são bem-vindas! Sinta-se livre para:

- 🐛 Reportar bugs ou erros
- 💡 Sugerir novos exemplos
- 📝 Melhorar a documentação
- ⭐ Dar uma estrela se achou útil!

## 📄 Licença

Este projeto está sob a licença MIT. Livre para uso educacional e comercial.

## 📊 Estatísticas

- **21 documentos** markdown
- **4400+ linhas** de documentação
- **50+ exemplos** práticos
- Cobertura de **17 estruturas** de dados

---

<div align="center">

**Feito com ❤️ para a comunidade Java**

[⬆ Voltar ao topo](#-guia-completo-de-estruturas-de-dados-em-java)

</div>
