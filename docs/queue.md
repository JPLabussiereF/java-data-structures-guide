# Queue (Fila)

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

Queue é uma interface que representa estruturas FIFO (First In, First Out), onde o primeiro elemento inserido é o primeiro a ser removido.

## 🔍 Implementações Comuns

- **LinkedList**: Implementação com lista encadeada
- **ArrayDeque**: Implementação com array circular (RECOMENDADA)
- **PriorityQueue**: Fila com prioridade (heap)

## ⚖️ Trade-offs

### ✅ Vantagens
- Operações O(1) nas pontas (offer, poll, peek)
- Ordem garantida (FIFO)
- Interface simples e clara
- Ideal para processamento sequencial

### ❌ Desvantagens
- Sem acesso aleatório
- Sem acesso ao meio da fila
- Implementação específica afeta performance

## 📊 Complexidade (Big O)

| Operação | LinkedList | ArrayDeque |
|----------|-----------|------------|
| offer (add) | O(1) | O(1) amortizado |
| poll (remove) | O(1) | O(1) |
| peek | O(1) | O(1) |
| size | O(1) | O(1) |

## 💻 Exemplos Práticos

### Exemplo 1: Fila Básica com ArrayDeque

```java
import java.util.ArrayDeque;
import java.util.Queue;

public class FilaBasica {
    public static void main(String[] args) {
        Queue<String> fila = new ArrayDeque<>();
        
        // Adiciona elementos
        fila.offer("Cliente 1");
        fila.offer("Cliente 2");
        fila.offer("Cliente 3");
        
        // Peek - vê o primeiro sem remover
        System.out.println("Próximo: " + fila.peek());
        
        // Poll - remove e retorna o primeiro
        while (!fila.isEmpty()) {
            System.out.println("Atendendo: " + fila.poll());
        }
    }
}
```

### Exemplo 2: Sistema de Atendimento

```java
import java.util.ArrayDeque;
import java.util.Queue;

class Cliente {
    String nome;
    int senha;
    
    Cliente(String nome, int senha) {
        this.nome = nome;
        this.senha = senha;
    }
    
    @Override
    public String toString() {
        return "Senha " + senha + " - " + nome;
    }
}

public class SistemaAtendimento {
    private Queue<Cliente> filaEspera = new ArrayDeque<>();
    private int proximaSenha = 1;
    
    public void adicionarCliente(String nome) {
        Cliente cliente = new Cliente(nome, proximaSenha++);
        filaEspera.offer(cliente);
        System.out.println("Cliente adicionado: " + cliente);
    }
    
    public void atenderProximo() {
        if (filaEspera.isEmpty()) {
            System.out.println("Fila vazia");
            return;
        }
        
        Cliente cliente = filaEspera.poll();
        System.out.println("Atendendo: " + cliente);
    }
    
    public void mostrarProximo() {
        if (filaEspera.isEmpty()) {
            System.out.println("Fila vazia");
        } else {
            System.out.println("Próximo: " + filaEspera.peek());
        }
    }
    
    public static void main(String[] args) {
        SistemaAtendimento sistema = new SistemaAtendimento();
        
        sistema.adicionarCliente("Alice");
        sistema.adicionarCliente("Bob");
        sistema.adicionarCliente("Carlos");
        
        sistema.mostrarProximo();
        sistema.atenderProximo();
        sistema.atenderProximo();
        sistema.mostrarProximo();
    }
}
```

### Exemplo 3: BFS (Busca em Largura) em Grafo

```java
import java.util.*;

public class BuscaEmLargura {
    static class Grafo {
        private Map<Integer, List<Integer>> adjacencias = new HashMap<>();
        
        void adicionarAresta(int origem, int destino) {
            adjacencias.putIfAbsent(origem, new ArrayList<>());
            adjacencias.putIfAbsent(destino, new ArrayList<>());
            adjacencias.get(origem).add(destino);
            adjacencias.get(destino).add(origem);
        }
        
        void bfs(int inicio) {
            Set<Integer> visitados = new HashSet<>();
            Queue<Integer> fila = new ArrayDeque<>();
            
            fila.offer(inicio);
            visitados.add(inicio);
            
            System.out.print("BFS a partir de " + inicio + ": ");
            
            while (!fila.isEmpty()) {
                int vertice = fila.poll();
                System.out.print(vertice + " ");
                
                // Adiciona vizinhos não visitados à fila
                for (int vizinho : adjacencias.get(vertice)) {
                    if (!visitados.contains(vizinho)) {
                        visitados.add(vizinho);
                        fila.offer(vizinho);
                    }
                }
            }
            System.out.println();
        }
    }
    
    public static void main(String[] args) {
        Grafo g = new Grafo();
        g.adicionarAresta(0, 1);
        g.adicionarAresta(0, 2);
        g.adicionarAresta(1, 3);
        g.adicionarAresta(1, 4);
        g.adicionarAresta(2, 5);
        g.adicionarAresta(2, 6);
        
        g.bfs(0);
    }
}
```

## 🎯 Quando Usar

- Processamento FIFO (primeiro a chegar, primeiro atendido)
- BFS em grafos
- Pool de tarefas
- Buffer de eventos
- Simulações (filas de atendimento)

## 🔗 Relacionados

- [ArrayDeque](./arraydeque.md) - Implementação recomendada
- [LinkedList](./linkedlist.md) - Implementação alternativa
- [PriorityQueue](./priorityqueue.md) - Fila com prioridade

---

[← Voltar ao Índice](../README.md)
