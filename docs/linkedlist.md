# LinkedList

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

LinkedList é uma implementação de lista duplamente encadeada que oferece performance superior para inserções e remoções, mas com custo de acesso mais lento.

## 🔍 Características

- Lista duplamente encadeada (cada nó tem referência para anterior e próximo)
- Implementa interfaces: `List`, `Deque`, `Queue`
- Não tem índice baseado em array
- Cada elemento é um objeto Node com dados e ponteiros
- Sem capacidade pré-definida (cresce conforme necessário)

## ⚖️ Trade-offs

### ✅ Vantagens

- **Inserção/remoção O(1)** quando você já tem a referência do nó
- **Inserção no início/final O(1)** sempre
- Não precisa de redimensionamento (sem cópias em massa)
- Excelente para implementar pilhas e filas
- Uso eficiente de memória para listas que mudam muito
- Pode funcionar como Deque (fila dupla)

### ❌ Desvantagens

- **Acesso aleatório O(n)** (precisa percorrer a lista)
- **Maior uso de memória** (cada elemento tem 2 referências extras)
- **Cache miss** frequente (nós não contíguos na memória)
- Performance geral inferior ao ArrayList para maioria dos casos
- Não é thread-safe

## 📊 Complexidade (Big O)

| Operação | Complexidade | Observações |
|----------|-------------|-------------|
| Acesso por índice | O(n) | Precisa percorrer até o índice |
| Busca | O(n) | Percorre sequencialmente |
| Inserção no início | O(1) | addFirst() |
| Inserção no final | O(1) | addLast() |
| Inserção no meio (por índice) | O(n) | Precisa achar posição + O(1) inserção |
| Remoção no início | O(1) | removeFirst() |
| Remoção no final | O(1) | removeLast() |
| Remoção no meio (por índice) | O(n) | Precisa achar posição + O(1) remoção |
| Remoção (com referência) | O(1) | Quando você já tem o iterator/nó |

## 💡 Quando Usar

### Use LinkedList quando:
- Inserções/remoções frequentes no início ou meio
- Implementar fila (Queue) ou pilha (Stack)
- Implementar fila dupla (Deque)
- Acesso sequencial é predominante
- Não precisa de acesso aleatório por índice
- Lista como buffer circular

### Caso de Uso Ideal:
```java
// Fila de processamento onde elementos entram no final e saem do início
LinkedList<Task> fila = new LinkedList<>();
fila.addLast(tarefa);  // O(1)
Task proxima = fila.removeFirst(); // O(1)
```

## ⚠️ Quando Evitar

### Evite LinkedList se:
- Acesso aleatório por índice é frequente
- Busca de elementos é comum
- A lista é pequena (< 100 elementos) - ArrayList é mais rápido
- Memória é limitada (overhead de ponteiros)
- Performance geral é crítica (ArrayList geralmente vence)

**Regra geral**: Na dúvida, use ArrayList. LinkedList só vence em cenários específicos.

## 💻 Exemplos Práticos

### Exemplo 1: Operações Básicas

```java
import java.util.LinkedList;

public class LinkedListBasico {
    public static void main(String[] args) {
        LinkedList<String> lista = new LinkedList<>();
        
        // Adição no final O(1)
        lista.add("Alice");
        lista.add("Bob");
        lista.addLast("Carlos"); // Equivalente a add()
        
        // Adição no início O(1)
        lista.addFirst("Diana"); // [Diana, Alice, Bob, Carlos]
        
        // Acesso - LENTO O(n)
        String primeiro = lista.get(0); // OK para poucos elementos
        String ultimo = lista.getLast(); // O(1) - otimizado
        
        // Remoção no início O(1)
        String removido = lista.removeFirst(); // "Diana"
        
        // Remoção no final O(1)
        lista.removeLast(); // Remove "Carlos"
        
        System.out.println(lista); // [Alice, Bob]
    }
}
```

### Exemplo 2: LinkedList como Fila (Queue)

```java
import java.util.LinkedList;
import java.util.Queue;

public class FilaComLinkedList {
    public static void main(String[] args) {
        // LinkedList implementa Queue - uso ideal!
        Queue<String> fila = new LinkedList<>();
        
        // Adiciona no final da fila O(1)
        fila.offer("Cliente 1");
        fila.offer("Cliente 2");
        fila.offer("Cliente 3");
        
        // Verifica o primeiro sem remover O(1)
        String proximo = fila.peek();
        System.out.println("Próximo a ser atendido: " + proximo);
        
        // Processa a fila (remove do início) O(1)
        while (!fila.isEmpty()) {
            String cliente = fila.poll();
            System.out.println("Atendendo: " + cliente);
        }
    }
}
```

### Exemplo 3: LinkedList como Pilha (Stack)

```java
import java.util.LinkedList;

public class PilhaComLinkedList {
    public static void main(String[] args) {
        // Usando LinkedList como Stack (LIFO)
        LinkedList<String> pilha = new LinkedList<>();
        
        // Push (adiciona no topo/início) O(1)
        pilha.push("Camada 1");
        pilha.push("Camada 2");
        pilha.push("Camada 3");
        
        // Peek (vê o topo sem remover) O(1)
        System.out.println("Topo: " + pilha.peek()); // Camada 3
        
        // Pop (remove do topo) O(1)
        while (!pilha.isEmpty()) {
            System.out.println("Removendo: " + pilha.pop());
        }
        // Saída: Camada 3, Camada 2, Camada 1
    }
}
```

### Exemplo 4: LinkedList como Deque (Fila Dupla)

```java
import java.util.Deque;
import java.util.LinkedList;

public class DequeComLinkedList {
    public static void main(String[] args) {
        // LinkedList implementa Deque - operações em ambas as pontas!
        Deque<Integer> deque = new LinkedList<>();
        
        // Adiciona em ambas as pontas O(1)
        deque.addFirst(1);    // [1]
        deque.addLast(2);     // [1, 2]
        deque.addFirst(0);    // [0, 1, 2]
        deque.addLast(3);     // [0, 1, 2, 3]
        
        // Remove de ambas as pontas O(1)
        System.out.println("Removido do início: " + deque.removeFirst()); // 0
        System.out.println("Removido do final: " + deque.removeLast());   // 3
        
        System.out.println("Deque atual: " + deque); // [1, 2]
        
        // Uso: buffer circular, sliding window, etc.
    }
}
```

### Exemplo 5: Comparação de Performance - ArrayList vs LinkedList

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

public class ComparacaoPerformance {
    public static void main(String[] args) {
        int quantidade = 100_000;
        
        // Teste 1: Inserção no início
        System.out.println("=== Inserção no início ===");
        testeInsercaoInicio(new ArrayList<>(), quantidade);
        testeInsercaoInicio(new LinkedList<>(), quantidade);
        
        // Teste 2: Inserção no final
        System.out.println("\n=== Inserção no final ===");
        testeInsercaoFinal(new ArrayList<>(), quantidade);
        testeInsercaoFinal(new LinkedList<>(), quantidade);
        
        // Teste 3: Acesso aleatório
        System.out.println("\n=== Acesso por índice ===");
        testeAcessoAleatorio(criarArrayList(quantidade), quantidade);
        testeAcessoAleatorio(criarLinkedList(quantidade), quantidade);
    }
    
    static void testeInsercaoInicio(List<Integer> lista, int n) {
        long inicio = System.currentTimeMillis();
        for (int i = 0; i < n; i++) {
            lista.add(0, i); // Adiciona sempre no início
        }
        long tempo = System.currentTimeMillis() - inicio;
        System.out.println(lista.getClass().getSimpleName() + ": " + tempo + " ms");
        // LinkedList ganha disparado aqui!
    }
    
    static void testeInsercaoFinal(List<Integer> lista, int n) {
        long inicio = System.currentTimeMillis();
        for (int i = 0; i < n; i++) {
            lista.add(i); // Adiciona no final
        }
        long tempo = System.currentTimeMillis() - inicio;
        System.out.println(lista.getClass().getSimpleName() + ": " + tempo + " ms");
        // ArrayList geralmente ganha ou empata
    }
    
    static void testeAcessoAleatorio(List<Integer> lista, int n) {
        long inicio = System.currentTimeMillis();
        long soma = 0;
        for (int i = 0; i < Math.min(n, 10000); i++) {
            soma += lista.get(i); // Acesso por índice
        }
        long tempo = System.currentTimeMillis() - inicio;
        System.out.println(lista.getClass().getSimpleName() + ": " + tempo + " ms");
        // ArrayList ganha MUITO aqui
    }
    
    static List<Integer> criarArrayList(int n) {
        List<Integer> lista = new ArrayList<>();
        for (int i = 0; i < n; i++) lista.add(i);
        return lista;
    }
    
    static List<Integer> criarLinkedList(int n) {
        List<Integer> lista = new LinkedList<>();
        for (int i = 0; i < n; i++) lista.add(i);
        return lista;
    }
}
```

### Exemplo 6: Iteração Eficiente

```java
import java.util.Iterator;
import java.util.LinkedList;

public class IteracaoLinkedList {
    public static void main(String[] args) {
        LinkedList<String> lista = new LinkedList<>();
        lista.add("A");
        lista.add("B");
        lista.add("C");
        lista.add("D");
        
        // RUIM: Acesso por índice O(n²)
        System.out.println("=== Forma LENTA (evite!) ===");
        long inicio = System.nanoTime();
        for (int i = 0; i < lista.size(); i++) {
            System.out.println(lista.get(i)); // Cada get() é O(n)!
        }
        System.out.println("Tempo: " + (System.nanoTime() - inicio) + " ns");
        
        // BOM: Enhanced for com Iterator O(n)
        System.out.println("\n=== Forma RÁPIDA (use esta!) ===");
        inicio = System.nanoTime();
        for (String item : lista) {
            System.out.println(item); // Iterator interno - O(1) por elemento
        }
        System.out.println("Tempo: " + (System.nanoTime() - inicio) + " ns");
        
        // TAMBÉM BOM: Iterator explícito
        Iterator<String> iter = lista.iterator();
        while (iter.hasNext()) {
            String item = iter.next();
            System.out.println(item);
            // Pode remover durante iteração
            if (item.equals("B")) {
                iter.remove(); // O(1)
            }
        }
    }
}
```

### Exemplo 7: Cenário Real - Buffer de Log Rotativo

```java
import java.util.LinkedList;

/**
 * Buffer rotativo de logs com tamanho máximo.
 * LinkedList é perfeita aqui: adiciona no final O(1) e remove do início O(1)
 */
public class LogBuffer {
    private final LinkedList<String> logs;
    private final int capacidadeMaxima;
    
    public LogBuffer(int capacidadeMaxima) {
        this.logs = new LinkedList<>();
        this.capacidadeMaxima = capacidadeMaxima;
    }
    
    public void adicionarLog(String mensagem) {
        // Adiciona no final O(1)
        logs.addLast(mensagem);
        
        // Se excedeu capacidade, remove o mais antigo O(1)
        if (logs.size() > capacidadeMaxima) {
            logs.removeFirst();
        }
    }
    
    public void imprimirLogs() {
        System.out.println("=== Últimos " + logs.size() + " logs ===");
        for (String log : logs) { // O(n) eficiente
            System.out.println(log);
        }
    }
    
    public static void main(String[] args) {
        LogBuffer buffer = new LogBuffer(5);
        
        // Simula adição de logs
        for (int i = 1; i <= 10; i++) {
            buffer.adicionarLog("Log #" + i + " - " + System.currentTimeMillis());
            try { Thread.sleep(100); } catch (InterruptedException e) {}
        }
        
        // Mantém apenas os últimos 5
        buffer.imprimirLogs();
    }
}
```

### Exemplo 8: Sistema de Undo/Redo

```java
import java.util.LinkedList;

/**
 * Sistema de Undo/Redo usando LinkedList como pilha.
 * Perfeito porque só opera no início (push/pop) - tudo O(1)
 */
public class EditorTexto {
    private String conteudo = "";
    private LinkedList<String> historico = new LinkedList<>();
    private LinkedList<String> redoStack = new LinkedList<>();
    
    public void escrever(String texto) {
        // Salva estado atual antes de modificar
        historico.push(conteudo); // O(1)
        conteudo += texto;
        redoStack.clear(); // Limpa redo após nova ação
        System.out.println("Conteúdo: " + conteudo);
    }
    
    public void undo() {
        if (historico.isEmpty()) {
            System.out.println("Nada para desfazer");
            return;
        }
        // Move estado atual para redo
        redoStack.push(conteudo); // O(1)
        // Restaura estado anterior
        conteudo = historico.pop(); // O(1)
        System.out.println("Após undo: " + conteudo);
    }
    
    public void redo() {
        if (redoStack.isEmpty()) {
            System.out.println("Nada para refazer");
            return;
        }
        // Move estado atual para histórico
        historico.push(conteudo); // O(1)
        // Restaura do redo
        conteudo = redoStack.pop(); // O(1)
        System.out.println("Após redo: " + conteudo);
    }
    
    public static void main(String[] args) {
        EditorTexto editor = new EditorTexto();
        
        editor.escrever("Olá ");
        editor.escrever("mundo");
        editor.escrever("!");
        
        editor.undo(); // Remove "!"
        editor.undo(); // Remove "mundo"
        editor.redo(); // Restaura "mundo"
        editor.escrever(" Java"); // "Olá mundo Java"
    }
}
```

### Exemplo 9: Quando LinkedList PERDE para ArrayList

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

public class QuandoLinkedListPerde {
    public static void main(String[] args) {
        demonstrarBuscaPorValor();
        demonstrarAcessoPorIndice();
        demonstrarInsercaoNoFinal();
    }
    
    static void demonstrarBuscaPorValor() {
        System.out.println("=== Busca por valor ===");
        int tamanho = 100_000;
        
        List<Integer> arrayList = new ArrayList<>();
        List<Integer> linkedList = new LinkedList<>();
        
        for (int i = 0; i < tamanho; i++) {
            arrayList.add(i);
            linkedList.add(i);
        }
        
        // Buscar elemento no meio
        long inicio = System.nanoTime();
        arrayList.contains(50_000);
        long tempoArray = System.nanoTime() - inicio;
        
        inicio = System.nanoTime();
        linkedList.contains(50_000);
        long tempoLinked = System.nanoTime() - inicio;
        
        System.out.println("ArrayList: " + tempoArray / 1000 + " μs");
        System.out.println("LinkedList: " + tempoLinked / 1000 + " μs");
        // ArrayList vence (melhor cache locality)
    }
    
    static void demonstrarAcessoPorIndice() {
        System.out.println("\n=== Acesso por índice ===");
        List<String> arrayList = new ArrayList<>();
        List<String> linkedList = new LinkedList<>();
        
        for (int i = 0; i < 10_000; i++) {
            arrayList.add("Item" + i);
            linkedList.add("Item" + i);
        }
        
        // Acesso aleatório
        long inicio = System.nanoTime();
        for (int i = 0; i < 1000; i++) {
            arrayList.get(i * 10);
        }
        long tempoArray = System.nanoTime() - inicio;
        
        inicio = System.nanoTime();
        for (int i = 0; i < 1000; i++) {
            linkedList.get(i * 10); // Precisa percorrer a cada vez!
        }
        long tempoLinked = System.nanoTime() - inicio;
        
        System.out.println("ArrayList: " + tempoArray / 1000 + " μs");
        System.out.println("LinkedList: " + tempoLinked / 1000 + " μs");
        // ArrayList ESMAGA LinkedList aqui
    }
    
    static void demonstrarInsercaoNoFinal() {
        System.out.println("\n=== Inserção no final ===");
        int tamanho = 100_000;
        
        long inicio = System.currentTimeMillis();
        List<Integer> arrayList = new ArrayList<>();
        for (int i = 0; i < tamanho; i++) {
            arrayList.add(i);
        }
        long tempoArray = System.currentTimeMillis() - inicio;
        
        inicio = System.currentTimeMillis();
        List<Integer> linkedList = new LinkedList<>();
        for (int i = 0; i < tamanho; i++) {
            linkedList.add(i);
        }
        long tempoLinked = System.currentTimeMillis() - inicio;
        
        System.out.println("ArrayList: " + tempoArray + " ms");
        System.out.println("LinkedList: " + tempoLinked + " ms");
        // ArrayList geralmente vence (ou empata) devido a cache
    }
}
```

## 🎯 Resumo de Decisão

```
Use ArrayList se:
✓ Acesso aleatório é comum
✓ Lista é relativamente estática
✓ Não tem certeza (padrão seguro)

Use LinkedList se:
✓ Inserções/remoções frequentes no início
✓ Implementando Queue/Deque
✓ Não precisa de acesso aleatório
✓ Operando sempre nas pontas
```

## 🔗 Relacionados

- [ArrayList](./arrays-arraylist.md) - Alternativa baseada em array
- [ArrayDeque](./arraydeque.md) - Melhor opção para Queue/Deque na maioria dos casos
- [Queue](./queue.md) - Interface de fila
- [Deque](./deque.md) - Interface de fila dupla

---

[← Voltar ao Índice](../README.md)
