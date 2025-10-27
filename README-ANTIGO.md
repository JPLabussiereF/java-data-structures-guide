# Guia Completo de Estruturas de Dados em Java

Um guia abrangente sobre estruturas de dados em Java, com análise detalhada de trade-offs, complexidades e exemplos práticos.

## 📚 Índice

### Estruturas Lineares
- [Arrays e ArrayList](./docs/arrays-arraylist.md)
- [LinkedList](./docs/linkedlist.md)
- [Stack (Pilha)](./docs/stack.md)
- [Queue (Fila)](./docs/queue.md)
- [Deque (Fila Dupla)](./docs/deque.md)

### Estruturas de Conjunto
- [HashSet](./docs/hashset.md)
- [LinkedHashSet](./docs/linkedhashset.md)
- [TreeSet](./docs/treeset.md)

### Estruturas de Mapa
- [HashMap](./docs/hashmap.md)
- [LinkedHashMap](./docs/linkedhashmap.md)
- [TreeMap](./docs/treemap.md)
- [Hashtable](./docs/hashtable.md)
- [ConcurrentHashMap](./docs/concurrenthashmap.md)

### Estruturas Especializadas
- [PriorityQueue (Heap)](./docs/priorityqueue.md)
- [ArrayDeque](./docs/arraydeque.md)

### Comparações e Guias
- [Comparação Geral de Todas as Estruturas](./docs/comparacao-geral.md)
- [Guia de Seleção: Qual Estrutura Usar?](./docs/guia-selecao.md)

## 🎯 Como Usar Este Guia

Cada documento contém:
- ✅ Características principais
- ⚖️ Trade-offs detalhados
- 📊 Análise de complexidade (Big O)
- 💡 Casos de uso ideais
- ⚠️ Quando evitar
- 💻 Exemplos práticos comentados

## 🚀 Início Rápido

**Novo aqui?** Comece pela [📋 Referência Rápida](./QUICK_REFERENCE.md) - decisão em 30 segundos!

**Precisa de ajuda para decidir?** Use o [✅ Checklist](./CHECKLIST.md)

**Quer mais detalhes?** Veja o [Guia de Seleção Completo](./docs/guia-selecao.md)

## 📖 Guias Principais

- **[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)** - Decisão rápida e tabela de complexidade
- **[CHECKLIST.md](./CHECKLIST.md)** - Perguntas para te ajudar a escolher
- **[COMPARACOES_CODIGO.md](./COMPARACOES_CODIGO.md)** - Exemplos lado a lado
- **[COMO_USAR.md](./COMO_USAR.md)** - Como navegar e usar este repositório
- **[Guia de Seleção](./docs/guia-selecao.md)** - Árvore de decisão detalhada
- **[Comparação Geral](./docs/comparacao-geral.md)** - Comparação completa de todas as estruturas

## 📖 Convenções

- **O(1)** - Tempo constante
- **O(log n)** - Tempo logarítmico
- **O(n)** - Tempo linear
- **O(n log n)** - Tempo linearítmico
- **O(n²)** - Tempo quadrático

## 🤝 Contribuições

Este é um guia educacional. Sinta-se livre para usar, compartilhar e adaptar conforme necessário.

## 📝 Licença

Livre para uso educacional e comercial.

## 🗺️ Mapa Visual das Estruturas

```
ESTRUTURAS DE DADOS JAVA
│
├─ 📚 LISTAS (Sequenciais)
│  ├─ Array[] ..................... Tamanho fixo, mais rápido
│  ├─ ArrayList ................... Tamanho dinâmico, acesso O(1)
│  └─ LinkedList .................. Inserções O(1) nas pontas
│
├─ 🎯 SETS (Elementos Únicos)
│  ├─ HashSet ..................... Mais rápido, sem ordem
│  ├─ LinkedHashSet ............... Mantém ordem de inserção
│  └─ TreeSet ..................... Sempre ordenado
│
├─ 🗂️ MAPS (Chave → Valor)
│  ├─ HashMap ..................... Mais rápido, sem ordem
│  ├─ LinkedHashMap ............... Mantém ordem de inserção
│  ├─ TreeMap ..................... Sempre ordenado
│  └─ ConcurrentHashMap ........... Thread-safe, alta performance
│
├─ 📥 QUEUES (Filas)
│  ├─ ArrayDeque .................. FIFO/LIFO, mais rápido
│  ├─ LinkedList .................. Implementa Queue
│  └─ PriorityQueue ............... Fila por prioridade (heap)
│
└─ 📤 STACK (Pilha)
   └─ ArrayDeque ................... Use como Deque (não use Stack class!)
```

## 🎓 Regras de Ouro

1. **Na dúvida, use ArrayList** (para listas)
2. **Na dúvida, use HashMap** (para mapas)
3. **ArrayDeque > Stack e LinkedList** (para pilhas e filas)
4. **HashSet > TreeSet** (se não precisa de ordem)
5. **NUNCA use**: Stack, Hashtable, Vector (são legados)

---

**Última atualização:** Outubro 2025
