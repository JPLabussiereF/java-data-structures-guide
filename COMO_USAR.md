# 📖 Como Usar Este Repositório

Este guia explica como navegar e aproveitar ao máximo este repositório de estruturas de dados.

## 🎯 Para Diferentes Perfis

### 👨‍🎓 Você é Estudante?

**Comece aqui:**
1. Leia o [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)
2. Estude cada estrutura em [docs/](./docs/)
3. Execute os exemplos no seu IDE
4. Use o [CHECKLIST.md](./CHECKLIST.md) ao praticar

**Sugestão de ordem de estudo:**
```
Semana 1: Arrays, ArrayList, LinkedList
Semana 2: HashMap, HashSet
Semana 3: TreeMap, TreeSet
Semana 4: Queue, Stack, Deque
Semana 5: PriorityQueue, ConcurrentHashMap
```

### 👨‍💻 Você é Desenvolvedor?

**Vai usar no seu projeto:**
1. Use o [CHECKLIST.md](./CHECKLIST.md) para decidir
2. Consulte [COMPARACOES_CODIGO.md](./COMPARACOES_CODIGO.md)
3. Veja exemplos na documentação específica
4. Copie e adapte o código

**Para problemas comuns:**
- Cache? → [HashMap](./docs/hashmap.md) ou [LinkedHashMap](./docs/linkedhashmap.md)
- Fila de tarefas? → [ArrayDeque](./docs/arraydeque.md)
- Contadores? → [HashMap](./docs/hashmap.md)
- LRU Cache? → [LinkedHashMap](./docs/linkedhashmap.md)

### 🎤 Você está se Preparando para Entrevistas?

**Foque nisso:**
1. [Comparação Geral](./docs/comparacao-geral.md) - Memorize as complexidades
2. [COMPARACOES_CODIGO.md](./COMPARACOES_CODIGO.md) - Pratique os exemplos
3. [Guia de Seleção](./docs/guia-selecao.md) - Aprenda a justificar escolhas

**Tópicos mais cobrados:**
- ✅ HashMap vs TreeMap vs LinkedHashMap
- ✅ ArrayList vs LinkedList
- ✅ HashSet para eliminar duplicatas
- ✅ PriorityQueue para Top K
- ✅ ArrayDeque como Stack/Queue

## 📂 Estrutura do Repositório

```
.
├── README.md                    # Índice principal
├── QUICK_REFERENCE.md          # Decisão rápida (comece aqui!)
├── CHECKLIST.md                # Perguntas interativas
├── COMPARACOES_CODIGO.md       # Exemplos lado a lado
├── COMO_USAR.md               # Este arquivo
└── docs/                       # Documentação detalhada
    ├── arrays-arraylist.md     # Arrays e ArrayList
    ├── linkedlist.md           # LinkedList
    ├── hashmap.md              # HashMap
    ├── hashset.md              # HashSet
    ├── treemap.md              # TreeMap
    ├── treeset.md              # TreeSet
    ├── arraydeque.md           # ArrayDeque
    ├── priorityqueue.md        # PriorityQueue
    ├── concurrenthashmap.md    # ConcurrentHashMap
    ├── ... (e outros)
    ├── comparacao-geral.md     # Tabelas comparativas
    └── guia-selecao.md         # Árvore de decisão
```

## 🔍 Como Encontrar o Que Você Precisa

### Busca por Problema

| Eu preciso... | Vá para |
|--------------|---------|
| Decidir rapidamente qual estrutura usar | [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) |
| Responder perguntas para decidir | [CHECKLIST.md](./CHECKLIST.md) |
| Ver código de exemplo lado a lado | [COMPARACOES_CODIGO.md](./COMPARACOES_CODIGO.md) |
| Entender trade-offs | Docs específica da estrutura |
| Ver complexidade (Big O) | [Comparação Geral](./docs/comparacao-geral.md) |
| Aprender a escolher | [Guia de Seleção](./docs/guia-selecao.md) |

### Busca por Estrutura

Todas as estruturas estão em [`docs/`](./docs/):
- Cada arquivo tem: características, trade-offs, complexidade, exemplos
- Formato: `nome-da-estrutura.md`
- Exemplo: [`hashmap.md`](./docs/hashmap.md)

## 💡 Dicas de Uso

### 1. Use os Links

Todos os documentos estão interligados. Clique nos links para navegar rapidamente.

### 2. Execute os Exemplos

Copie os exemplos e execute no seu IDE:
```java
// Exemplo dos docs pode ser copiado diretamente
Map<String, Integer> mapa = new HashMap<>();
mapa.put("teste", 1);
```

### 3. Marque seus Favoritos

Adicione aos favoritos:
- [QUICK_REFERENCE.md](./QUICK_REFERENCE.md) - Consulta rápida
- [CHECKLIST.md](./CHECKLIST.md) - Para decisões
- A documentação das estruturas que você mais usa

### 4. Use o GitHub Search

Pressione `/` no GitHub e busque por termos:
- "O(1)" - Encontra operações constantes
- "thread-safe" - Encontra estruturas concorrentes
- "exemplo" - Encontra códigos de exemplo

## 🎓 Planos de Estudo

### Plano Básico (1 semana)

**Dia 1-2:** Listas
- [Arrays e ArrayList](./docs/arrays-arraylist.md)
- [LinkedList](./docs/linkedlist.md)
- Exercício: Implementar uma lista de tarefas

**Dia 3-4:** Maps
- [HashMap](./docs/hashmap.md)
- [TreeMap](./docs/treemap.md)
- Exercício: Contador de palavras

**Dia 5-6:** Sets e Queues
- [HashSet](./docs/hashset.md)
- [ArrayDeque](./docs/arraydeque.md)
- Exercício: Sistema de fila de atendimento

**Dia 7:** Revisão
- [Comparação Geral](./docs/comparacao-geral.md)
- [Guia de Seleção](./docs/guia-selecao.md)

### Plano Intermediário (2 semanas)

Siga o plano básico +

**Semana 2:**
- [LinkedHashMap](./docs/linkedhashmap.md) + LRU Cache
- [LinkedHashSet](./docs/linkedhashset.md)
- [TreeSet](./docs/treeset.md)
- [PriorityQueue](./docs/priorityqueue.md)
- [ConcurrentHashMap](./docs/concurrenthashmap.md)

### Plano Avançado (1 mês)

Semanas 1-2: Plano intermediário

**Semana 3:** Casos de uso avançados
- Implementar LRU Cache
- Implementar Top K elementos
- BFS e DFS com estruturas corretas
- Sistema de processamento de eventos

**Semana 4:** Otimização
- Análise de performance
- Benchmarking
- Trade-offs em produção

## 🔧 Ferramentas Úteis

### JMH para Benchmarks

```java
// Adicione ao pom.xml
<dependency>
    <groupId>org.openjdk.jmh</groupId>
    <artifactId>jmh-core</artifactId>
    <version>1.36</version>
</dependency>
```

### VisualVM para Análise de Memória

- Veja uso de memória real
- Compare estruturas
- Identifique gargalos

## ❓ FAQ

### Qual arquivo ler primeiro?

**[QUICK_REFERENCE.md](./QUICK_REFERENCE.md)** - Tem tudo resumido em uma página.

### Preciso ler tudo?

**Não!** Leia o que você precisa:
- Desenvolvendo? Use o [CHECKLIST.md](./CHECKLIST.md)
- Estudando? Siga um plano de estudo
- Entrevista? Foque em [Comparação Geral](./docs/comparacao-geral.md)

### Os exemplos funcionam?

**Sim!** Todos os exemplos são testados e funcionais. Copie e cole no seu IDE.

### Como contribuir?

Veja a seção de contribuição no [README.md](./README.md).

## 🎯 Próximos Passos

Agora que você sabe como usar o repositório:

1. ✅ Escolha seu perfil (estudante/desenvolvedor/entrevista)
2. ✅ Siga o plano sugerido
3. ✅ Pratique com os exemplos
4. ✅ Consulte quando precisar

**Comece agora:**
- 👉 [QUICK_REFERENCE.md](./QUICK_REFERENCE.md)
- 👉 [CHECKLIST.md](./CHECKLIST.md)

---

**Dica:** Adicione este repositório aos favoritos do GitHub (⭐) para encontrar facilmente!
