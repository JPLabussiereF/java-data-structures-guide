# Stack (Pilha)

[← Voltar ao Índice](../README.md)

## 📋 Visão Geral

Stack é uma estrutura de dados LIFO (Last In, First Out) onde o último elemento inserido é o primeiro a ser removido. Em Java, pode ser implementada usando a classe `Stack` (legada) ou usando `Deque`.

## 🔍 Características

- **LIFO**: Last In, First Out (último a entrar, primeiro a sair)
- Operações principais: push (empilhar), pop (desempilhar), peek (ver o topo)
- Classe `Stack` herda de `Vector` (sincronizada e legada)
- **Recomendação moderna**: Use `Deque` (ArrayDeque ou LinkedList) ao invés de `Stack`

## ⚖️ Trade-offs

### ✅ Vantagens

- Operações O(1) no topo da pilha
- Simples e intuitiva para algoritmos LIFO
- Útil para recursão, backtracking, parsing
- Gerenciamento automático de escopo

### ❌ Desvantagens

**Stack (classe legada):**
- Herda de Vector (thread-safe desnecessariamente - overhead)
- Design ruim (viola princípios OO)
- Performance inferior ao ArrayDeque
- Considerada obsoleta

**Em geral:**
- Acesso apenas ao topo (sem acesso aleatório)
- Não é ideal para busca de elementos
- Overflow se implementação tem limite

## 📊 Complexidade (Big O)

| Operação | Stack | ArrayDeque (recomendado) |
|----------|-------|--------------------------|
| Push (empilhar) | O(1)* | O(1) amortizado |
| Pop (desempilhar) | O(1) | O(1) |
| Peek (ver topo) | O(1) | O(1) |
| Search (buscar) | O(n) | O(n) |
| isEmpty | O(1) | O(1) |

*Stack pode ter overhead de sincronização

## 💡 Quando Usar

### Use Stack quando:
- Precisa de comportamento LIFO estrito
- Implementar backtracking (labirintos, puzzles)
- Avaliar expressões matemáticas
- Validar parênteses/brackets
- Manter histórico de ações (undo)
- Navegação para trás (histórico de browser)
- Parsing e compiladores

### ⚠️ Preferência de Implementação:
```java
// EVITE (legado):
Stack<String> stack = new Stack<>();

// PREFIRA (moderno):
Deque<String> stack = new ArrayDeque<>();
```

## ⚠️ Quando Evitar

- Quando precisa acessar elementos no meio
- Se precisa de ordem FIFO (use Queue)
- Quando sincronização não é necessária mas usa Stack class
- Para grandes volumes onde cache locality importa (considere ArrayList)

## 💻 Exemplos Práticos

### Exemplo 1: Stack Legado (EVITE)

```java
import java.util.Stack;

public class StackLegado {
    public static void main(String[] args) {
        // Classe legada - EVITE usar em código novo
        Stack<String> pilha = new Stack<>();
        
        // Push - adiciona no topo O(1)
        pilha.push("Primeiro");
        pilha.push("Segundo");
        pilha.push("Terceiro");
        
        // Peek - vê o topo sem remover O(1)
        System.out.println("Topo: " + pilha.peek()); // Terceiro
        
        // Pop - remove do topo O(1)
        System.out.println("Removido: " + pilha.pop()); // Terceiro
        System.out.println("Removido: " + pilha.pop()); // Segundo
        
        // Verifica se está vazia
        System.out.println("Vazia? " + pilha.isEmpty()); // false
        
        // Search - retorna posição (1-based) do topo
        pilha.push("A");
        pilha.push("B");
        System.out.println("Posição de 'A': " + pilha.search("A")); // 2
        // Nota: search() é 1-based e do topo para baixo!
    }
}
```

### Exemplo 2: Stack Moderno com ArrayDeque (RECOMENDADO)

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class StackModerno {
    public static void main(String[] args) {
        // Forma moderna e eficiente
        Deque<String> pilha = new ArrayDeque<>();
        
        // Push - adiciona no topo O(1)
        pilha.push("Primeiro");
        pilha.push("Segundo");
        pilha.push("Terceiro");
        
        // Peek - vê o topo sem remover O(1)
        System.out.println("Topo: " + pilha.peek()); // Terceiro
        
        // Pop - remove do topo O(1)
        while (!pilha.isEmpty()) {
            System.out.println("Removido: " + pilha.pop());
        }
        // Saída: Terceiro, Segundo, Primeiro (LIFO)
    }
}
```

### Exemplo 3: Validar Parênteses Balanceados

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class ValidarParenteses {
    public static boolean isBalanceado(String expressao) {
        Deque<Character> pilha = new ArrayDeque<>();
        
        for (char c : expressao.toCharArray()) {
            // Se é abertura, empilha
            if (c == '(' || c == '[' || c == '{') {
                pilha.push(c);
            }
            // Se é fechamento, verifica
            else if (c == ')' || c == ']' || c == '}') {
                if (pilha.isEmpty()) {
                    return false; // Fechamento sem abertura
                }
                
                char topo = pilha.pop();
                
                // Verifica se o par corresponde
                if ((c == ')' && topo != '(') ||
                    (c == ']' && topo != '[') ||
                    (c == '}' && topo != '{')) {
                    return false;
                }
            }
        }
        
        // Se sobrou algo na pilha, está desbalanceado
        return pilha.isEmpty();
    }
    
    public static void main(String[] args) {
        String[] testes = {
            "()",           // true
            "()[]{}",       // true
            "(]",           // false
            "([)]",         // false
            "{[()]}",       // true
            "(((",          // false
            "((()))",       // true
        };
        
        for (String teste : testes) {
            System.out.println(teste + " é balanceado? " + isBalanceado(teste));
        }
    }
}
```

### Exemplo 4: Avaliar Expressão Pós-Fixada (RPN)

```java
import java.util.ArrayDeque;
import java.util.Deque;

/**
 * Avalia expressões em notação polonesa reversa (RPN)
 * Exemplo: "3 4 + 2 *" = (3 + 4) * 2 = 14
 */
public class AvaliarRPN {
    public static int avaliar(String[] tokens) {
        Deque<Integer> pilha = new ArrayDeque<>();
        
        for (String token : tokens) {
            switch (token) {
                case "+":
                    pilha.push(pilha.pop() + pilha.pop());
                    break;
                case "-":
                    int b = pilha.pop();
                    int a = pilha.pop();
                    pilha.push(a - b);
                    break;
                case "*":
                    pilha.push(pilha.pop() * pilha.pop());
                    break;
                case "/":
                    int divisor = pilha.pop();
                    int dividendo = pilha.pop();
                    pilha.push(dividendo / divisor);
                    break;
                default:
                    // É um número
                    pilha.push(Integer.parseInt(token));
            }
        }
        
        return pilha.pop();
    }
    
    public static void main(String[] args) {
        // Exemplo: (3 + 4) * 2 = 14
        String[] expressao1 = {"3", "4", "+", "2", "*"};
        System.out.println("Resultado: " + avaliar(expressao1)); // 14
        
        // Exemplo: (15 / (7 - (1 + 1))) * 3 = 9
        String[] expressao2 = {"15", "7", "1", "1", "+", "-", "/", "3", "*"};
        System.out.println("Resultado: " + avaliar(expressao2)); // 9
        
        // Exemplo: 5 + ((1 + 2) * 4) - 3 = 14
        String[] expressao3 = {"5", "1", "2", "+", "4", "*", "+", "3", "-"};
        System.out.println("Resultado: " + avaliar(expressao3)); // 14
    }
}
```

### Exemplo 5: Histórico de Navegação (Browser Back)

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class HistoricoNavegador {
    private Deque<String> historico = new ArrayDeque<>();
    private Deque<String> historicoFrente = new ArrayDeque<>();
    private String paginaAtual;
    
    public void visitar(String url) {
        if (paginaAtual != null) {
            historico.push(paginaAtual);
        }
        paginaAtual = url;
        historicoFrente.clear(); // Limpa "frente" ao visitar nova página
        System.out.println("Visitando: " + url);
    }
    
    public void voltar() {
        if (historico.isEmpty()) {
            System.out.println("Não há páginas anteriores");
            return;
        }
        
        historicoFrente.push(paginaAtual);
        paginaAtual = historico.pop();
        System.out.println("Voltou para: " + paginaAtual);
    }
    
    public void avancar() {
        if (historicoFrente.isEmpty()) {
            System.out.println("Não há páginas à frente");
            return;
        }
        
        historico.push(paginaAtual);
        paginaAtual = historicoFrente.pop();
        System.out.println("Avançou para: " + paginaAtual);
    }
    
    public void mostrarAtual() {
        System.out.println("Página atual: " + paginaAtual);
    }
    
    public static void main(String[] args) {
        HistoricoNavegador browser = new HistoricoNavegador();
        
        browser.visitar("google.com");
        browser.visitar("github.com");
        browser.visitar("stackoverflow.com");
        
        browser.voltar();  // Volta para github.com
        browser.voltar();  // Volta para google.com
        
        browser.avancar(); // Avança para github.com
        
        browser.visitar("reddit.com"); // Limpa histórico da frente
        
        browser.voltar();  // Volta para github.com
        browser.avancar(); // Avança para reddit.com
    }
}
```

### Exemplo 6: Conversão Infixo para Pós-fixo

```java
import java.util.ArrayDeque;
import java.util.Deque;

/**
 * Converte expressões infixas (3 + 4) para pós-fixas (3 4 +)
 * Usando o algoritmo Shunting Yard de Dijkstra
 */
public class InfixoParaPosFixo {
    
    private static int precedencia(char operador) {
        switch (operador) {
            case '+':
            case '-':
                return 1;
            case '*':
            case '/':
                return 2;
            case '^':
                return 3;
            default:
                return -1;
        }
    }
    
    private static boolean isOperador(char c) {
        return c == '+' || c == '-' || c == '*' || c == '/' || c == '^';
    }
    
    public static String converter(String infixa) {
        StringBuilder resultado = new StringBuilder();
        Deque<Character> pilha = new ArrayDeque<>();
        
        for (int i = 0; i < infixa.length(); i++) {
            char c = infixa.charAt(i);
            
            // Se é espaço, ignora
            if (c == ' ') continue;
            
            // Se é número/letra, adiciona ao resultado
            if (Character.isLetterOrDigit(c)) {
                resultado.append(c).append(' ');
            }
            // Se é abre parênteses, empilha
            else if (c == '(') {
                pilha.push(c);
            }
            // Se é fecha parênteses, desempilha até achar '('
            else if (c == ')') {
                while (!pilha.isEmpty() && pilha.peek() != '(') {
                    resultado.append(pilha.pop()).append(' ');
                }
                pilha.pop(); // Remove o '('
            }
            // Se é operador
            else if (isOperador(c)) {
                while (!pilha.isEmpty() && 
                       precedencia(c) <= precedencia(pilha.peek())) {
                    resultado.append(pilha.pop()).append(' ');
                }
                pilha.push(c);
            }
        }
        
        // Desempilha operadores restantes
        while (!pilha.isEmpty()) {
            resultado.append(pilha.pop()).append(' ');
        }
        
        return resultado.toString().trim();
    }
    
    public static void main(String[] args) {
        String[] expressoes = {
            "A + B",
            "A + B * C",
            "(A + B) * C",
            "A * B + C",
            "A + B + C",
            "(A + B) * (C - D)",
            "A * (B + C) / D"
        };
        
        for (String exp : expressoes) {
            System.out.println("Infixa:   " + exp);
            System.out.println("Pós-fixa: " + converter(exp));
            System.out.println();
        }
    }
}
```

### Exemplo 7: Verificar Caminho Válido em Diretório

```java
import java.util.ArrayDeque;
import java.util.Deque;

/**
 * Simplifica caminhos de diretório como no Unix
 * Exemplo: "/a/./b/../../c/" -> "/c"
 */
public class SimplificarCaminho {
    public static String simplificar(String caminho) {
        Deque<String> pilha = new ArrayDeque<>();
        String[] partes = caminho.split("/");
        
        for (String parte : partes) {
            // Ignora vazios e "."
            if (parte.isEmpty() || parte.equals(".")) {
                continue;
            }
            // ".." volta um diretório
            else if (parte.equals("..")) {
                if (!pilha.isEmpty()) {
                    pilha.pop();
                }
            }
            // Nome de diretório válido
            else {
                pilha.push(parte);
            }
        }
        
        // Reconstrói o caminho
        if (pilha.isEmpty()) {
            return "/";
        }
        
        StringBuilder resultado = new StringBuilder();
        // Pilha está invertida, então precisamos inverter
        Deque<String> temp = new ArrayDeque<>(pilha);
        while (!temp.isEmpty()) {
            resultado.insert(0, "/" + temp.pop());
        }
        
        return resultado.toString();
    }
    
    public static void main(String[] args) {
        String[] caminhos = {
            "/home/",
            "/../",
            "/home//foo/",
            "/a/./b/../../c/",
            "/a/../../b/../c//.//",
            "/a//b////c/d//././/.."
        };
        
        for (String caminho : caminhos) {
            System.out.println(caminho + " -> " + simplificar(caminho));
        }
    }
}
```

### Exemplo 8: Sistema de Undo/Redo

```java
import java.util.ArrayDeque;
import java.util.Deque;

/**
 * Sistema de Undo/Redo para editor de texto
 */
class Comando {
    String acao;
    String dado;
    
    Comando(String acao, String dado) {
        this.acao = acao;
        this.dado = dado;
    }
    
    @Override
    public String toString() {
        return acao + ": " + dado;
    }
}

public class SistemaUndoRedo {
    private Deque<Comando> pilhaUndo = new ArrayDeque<>();
    private Deque<Comando> pilhaRedo = new ArrayDeque<>();
    
    public void executar(Comando comando) {
        System.out.println("Executando: " + comando);
        pilhaUndo.push(comando);
        pilhaRedo.clear(); // Nova ação limpa o redo
    }
    
    public void undo() {
        if (pilhaUndo.isEmpty()) {
            System.out.println("Nada para desfazer");
            return;
        }
        
        Comando comando = pilhaUndo.pop();
        pilhaRedo.push(comando);
        System.out.println("Desfazendo: " + comando);
    }
    
    public void redo() {
        if (pilhaRedo.isEmpty()) {
            System.out.println("Nada para refazer");
            return;
        }
        
        Comando comando = pilhaRedo.pop();
        pilhaUndo.push(comando);
        System.out.println("Refazendo: " + comando);
    }
    
    public void mostrarEstado() {
        System.out.println("\n=== Estado Atual ===");
        System.out.println("Undo disponível: " + !pilhaUndo.isEmpty());
        System.out.println("Redo disponível: " + !pilhaRedo.isEmpty());
        System.out.println();
    }
    
    public static void main(String[] args) {
        SistemaUndoRedo sistema = new SistemaUndoRedo();
        
        sistema.executar(new Comando("Escrever", "Olá"));
        sistema.executar(new Comando("Escrever", " Mundo"));
        sistema.executar(new Comando("Deletar", " Mundo"));
        
        sistema.mostrarEstado();
        
        sistema.undo(); // Desfaz deletar
        sistema.undo(); // Desfaz escrever " Mundo"
        
        sistema.mostrarEstado();
        
        sistema.redo(); // Refaz escrever " Mundo"
        
        sistema.executar(new Comando("Escrever", "!")); // Limpa redo
        
        sistema.mostrarEstado();
    }
}
```

## 🎯 Resumo de Decisão

```
SEMPRE use Deque ao invés de Stack:

// ❌ EVITE
Stack<String> pilha = new Stack<>();

// ✅ USE
Deque<String> pilha = new ArrayDeque<>();  // Melhor performance
// ou
Deque<String> pilha = new LinkedList<>();  // Se precisa de iterator bidirecional
```

## 🔗 Relacionados

- [Queue](./queue.md) - Estrutura FIFO
- [Deque](./deque.md) - Interface moderna para Stack/Queue
- [ArrayDeque](./arraydeque.md) - Implementação recomendada

---

[← Voltar ao Índice](../README.md)
